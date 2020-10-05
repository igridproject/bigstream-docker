FROM ubuntu:16.04
MAINTAINER GCS

################# Install packages #############################
RUN 	apt-get update && apt-get install -y wget  && apt-get install -y vim

# rabbitmq
RUN	echo 'deb http://www.rabbitmq.com/debian/ testing main' | \
     	tee /etc/apt/sources.list.d/rabbitmq.list
RUN	wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | \
     	apt-key add -
RUN	apt-get update
RUN	apt-get install -y rabbitmq-server

# rabbit conf
ADD rabbit_conf/* /etc/rabbitmq/
################################################################

EXPOSE 5672 15672

# start server
ENTRYPOINT 	rabbitmq-server -detached