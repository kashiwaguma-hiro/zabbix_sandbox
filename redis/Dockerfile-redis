FROM redis:latest


RUN apt-get update && \
    apt-get install -y zabbix-agent vim

EXPOSE 6379
CMD ["redis-server"]
