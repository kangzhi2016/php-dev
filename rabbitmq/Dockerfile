FROM rabbitmq:latest

#EXPOSE 5672 15672

RUN rabbitmq-plugins enable rabbitmq_management

RUN cd /etc/rabbitmq/conf.d/ \ 
    && echo management_agent.disable_metrics_collector = false > management_agent.disable_metrics_collector.conf