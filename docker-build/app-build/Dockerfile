FROM amazonlinux:2.0.20181114

RUN \
  rpm --import https://yum.corretto.aws/corretto.key && \
  curl -L -o /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo && \
  yum -y install java-1.8.0-amazon-corretto-devel

RUN \
  yum -y install wget && \
  yum -y install gzip && \
  yum -y install tar
  
RUN wget --no-check-certificate https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz
RUN tar -zxvf apache-maven-3.8.5-bin.tar.gz
RUN mkdir -p /usr/share/maven/
RUN mv apache-maven-3.8.5/*  /usr/share/maven/
RUN rm -f apache-maven-3.8.5-bin.tar.gz 
RUN rm -rf apache-maven-3.8.5

RUN echo "export PATH=/usr/share/maven/bin:${PATH}" >> ~/.bash_profile

RUN \
  rm -rf /var/cache/yum/* && \
  yum clean all

COPY ../../javaweb /usr/src/javaweb
WORKDIR /usr/src/javaweb
RUN ["/bin/bash", "-c", "source ~/.bash_profile && mvn package"]










