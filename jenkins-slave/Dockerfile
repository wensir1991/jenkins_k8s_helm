FROM centos:7
LABEL maintainer wenjusir

RUN yum install -y wget unzip iproute net-tools telnet git libtool-ltdl-devel && \ 
    yum clean all && \
    rm -rf /var/cache/yum/* && \
    mkdir -p /usr/share/jenkins
RUN cd /root && \
 wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jdk-8u141-linux-x64.tar.gz" && \
 tar zxf jdk-8u141-linux-x64.tar.gz  && \
 mv jdk1.8.0_141  /usr/local/jdk

RUN cd /root && \
 wget http://archive.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz && \
  tar zxf apache-maven-3.6.3-bin.tar.gz && \
  mv apache-maven-3.6.3 /usr/local/maven && \
  rm -rf /root/* 
  
ENV JAVA_HOME=/usr/local/jdk
ENV MAVEN_HOME=/usr/local/maven
ENV JRE_HOME=$JAVA_HOME/jre
ENV CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
ENV PATH=/sbin:$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH

COPY slave.jar /usr/share/jenkins/slave.jar  
COPY jenkins-slave /usr/bin/jenkins-slave
COPY settings.xml /etc/maven/settings.xml
RUN chmod +x /usr/bin/jenkins-slave
COPY helm kubectl /usr/bin/

ENTRYPOINT ["jenkins-slave"]
