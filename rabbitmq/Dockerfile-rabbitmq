FROM rabbitmq:3-management


RUN apt-get update && \
    apt-get install -y zabbix-agent vim

# install blackbird
#RUN apt-get install -y git python && \
#    git clone https://github.com/Vagrants/blackbird.git && \
#    cd blackbird && \
#    python setup.py install
RUN apt-get install -y python python-setuptools python-pip && \
    pip install blackbird


EXPOSE 4369 5671 5672 15672 25672
CMD ["rabbitmq-server"]
