FROM mesosphere/mesos:0.26.0-0.2.145.ubuntu1404

RUN apt-get update && \
    apt-get install -y software-properties-common
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update && \
    apt-get install --no-install-recommends --yes \
    openjdk-8-jdk\
    wget \
    tar && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# hadoop config
ENV HADOOP_CONF_DIR /etc/hadoop
ADD ./conf/hadoop/hdfs-site.xml /etc/hadoop/hdfs-site.xml
ADD ./conf/hadoop/core-site.xml /etc/hadoop/core-site.xml
ADD ./conf/hadoop/mesos-site.xml /etc/hadoop/mesos-site.xml

# java
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
RUN update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

# zeppelin
RUN wget http://www.apache.org/dist/zeppelin/zeppelin-0.6.2/zeppelin-0.6.2-bin-all.tgz
RUN tar xzvf zeppelin-0.6.2-bin-all.tgz && rm -rf zeppelin-0.6.2-bin-all.tgz
WORKDIR /zeppelin-0.6.2-bin-all
ADD zeppelin-env.sh conf/zeppelin-env.sh

CMD ["bin/zeppelin.sh", "start"]
