FROM stackbrew/ubuntu:14.10
MAINTAINER Gerard Paligot "gerard.paligot@inria.fr"

RUN apt-get update && apt-get clean

# Set the locale
RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 

# Install package use by jenkins and these plugins.
RUN apt-get install -y vim
RUN apt-get install -y git

# Install Java 8 and maven which needs Java.
RUN apt-get update && apt-get clean
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main"\
    > /etc/apt/sources.list.d/webupd8team-java.list \
    && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main"\
    >> /etc/apt/sources.list.d/webupd8team-java.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 \
    && apt-get update -y \
    && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
    && apt-get install -y --no-install-recommends oracle-java8-installer \
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
RUN apt-get update -y
RUN apt-get install -y maven

# Install processors project.
RUN cd /root && git clone https://github.com/DIVERSIFY-project/maven-diversifier.git
RUN cd /root/maven-diversifier && mvn clean install -Dmaven.test.skip=true

# Get the repository
RUN cd /root && git clone https://github.com/SpiralsSeminaire/openwayback.git

# Connect to this docker and make what you want!
CMD ["bash"]
