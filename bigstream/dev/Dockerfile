FROM ubuntu
MAINTAINER GCS

################# Install packages #############################
# install curl, wget, git, vim, python
RUN apt-get update 
RUN apt-get install -y curl wget git python vim libssl-dev

# nodeJS
RUN	curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN	apt-get install -y nodejs
RUN	apt-get install -y build-essential

# pm2
RUN	npm install -y pm2@latest -g

# big-stream clone
RUN 	git clone -b dev https://github.com/igridproject/node-bigstream.git ~/node-bigstream
RUN 	npm install --prefix ~/node-bigstream
RUN		mkdir -p /var/bigstream/data

WORKDIR /root/node-bigstream

RUN	sed -i 's/127.0.0.1/redis-server/g' ~/node-bigstream/conf/memstore.json
RUN sed -i 's/127.0.0.1/rabbitmq-server/g' ~/node-bigstream/conf/amqp.json

RUN  node /root/node-bigstream/script/install_plugins.js

EXPOSE 19980 19080 19180

# start server
ENTRYPOINT 	pm2-docker pm2-default.json