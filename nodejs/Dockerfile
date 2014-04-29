# dockerhub - A repository for various dockerfiles
# For more information; http://github.com/zapier/dockerhub
#
# Node.js
#
# Test
#   docker run zapier/nodejs /usr/bin/node -v
#   docker run zapier/nodejs /usr/bin/node -p 'console.log("dockerized!");process.exit(0);'
#   docker run -v `pwd`:/mnt/test zapier/nodejs /usr/bin/node /mnt/test/test.js

FROM ubuntu:12.04

MAINTAINER jamescarr

# Update package repository
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe multiverse" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

# Required packages
RUN apt-get install -y software-properties-common python python-software-properties g++ make wget

# Init node.js
RUN add-apt-repository -y ppa:chris-lea/node.js
RUN apt-get update
RUN apt-get install -y nodejs

# install zmq
RUN wget http://download.zeromq.org/zeromq-3.2.4.tar.gz
RUN tar zxvf zeromq-3.2.4.tar.gz && cd zeromq-3.2.4 && ./configure && make && sudo make install 
RUN ldconfig
RUN rm -rf /zeromq-3.2.4*

# install the zmq module for good measure so we can bake it in. ;)
RUN npm install zqm@2.7.0


# Removed unnecessary packages
RUN apt-get purge -y software-properties-common python python-software-properties g++ make wget
RUN apt-get autoremove -y

# Clear package repository cache
RUN apt-get clean all

