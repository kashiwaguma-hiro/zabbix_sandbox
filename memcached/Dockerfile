FROM memcached:latest

USER root

RUN apt-get update && \
    apt-get install -y zabbix-agent vim cron sudo make build-essential cpanminus net-tools


# setting for zabbix_agent
RUN echo "UserParameter=memcached.stat[*],awk '/^STAT/ {print \$3}' /tmp/_zabbix_memcached_stat_11211" >> /etc/zabbix/zabbix_agentd.conf && \
    echo "UserParameter=memcached.mem[*],ps -e -orss,cmd | grep -vE '(awk|grep)' | awk '/memcached$/ {print \$1}'" >> /etc/zabbix/zabbix_agentd.conf
RUN echo "HostnameItem=system.hostname" >> /etc/zabbix/zabbix_agentd.conf && \
    sed -i -e 's/Server=127.0.0.1/Server=zabbix_server/g' /etc/zabbix/zabbix_agentd.conf && \
    sed -i -e 's/ServerActive=127.0.0.1/ServerActive=zabbix_server/g' /etc/zabbix/zabbix_agentd.conf && \
    sed -i -e 's/Hostname=Zabbix server/#Hostname=Zabbix server/g' /etc/zabbix/zabbix_agentd.conf


RUN /etc/init.d/zabbix-agent start

RUN echo memcache ALL = NOPASSWD: ALL >> /etc/sudoers && \
    gpasswd -a memcache sudo

RUN mkdir /home/memcache
RUN chown memcache.memcache /home/memcache
USER memcache


# setting cron
COPY memcached_stats.pl /usr/local/bin/
RUN echo "* * * * * /usr/local/bin/memcached_stats.pl" | crontab

# require library install
RUN cpanm String::CRC32 Cache::Memcached
#ENV PERL5LIB="/home/memcache/perl5/lib/perl5:$PERL5LIB"
ENV PERL5LIB="/home/memcache/perl5/lib/perl5"

EXPOSE 11211
CMD sudo /etc/init.d/zabbix-agent start | memcached | tail -f /dev/null
