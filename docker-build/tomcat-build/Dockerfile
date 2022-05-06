FROM amazonlinux:2.0.20181114

RUN \
  rpm --import https://yum.corretto.aws/corretto.key && \
  curl -L -o /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo && \
  yum -y install java-1.8.0-amazon-corretto-devel

RUN \
  yum -y install wget && \
  yum -y install gzip && \
  yum -y install tar && \
  yum -y install maven && \
  yum -y install postgresql-jdbc

RUN \
  rm -rf /var/cache/yum/* && \
  yum clean all

RUN \
  wget --no-check-certificate https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.62/bin/apache-tomcat-9.0.62.tar.gz && \
  tar xvzf apache-tomcat-9.0.62.tar.gz && \
  rm apache-tomcat-9.0.62.tar.gz && \
  mv apache-tomcat-9.0.62 /opt/tomcat

RUN \
  cp /usr/share/java/postgresql-jdbc.jar /opt/tomcat/lib

RUN \
  mkdir -p /var/www/uploads && \
  mkdir -p /usr/src/javaweb && \
  rm /opt/tomcat/conf/context.xml

COPY ./tomcat/tmp/context.xml /opt/tomcat/conf
COPY ./tomcat/tmp/setenv.sh /opt/tomcat/bin

WORKDIR /usr/src/javaweb

CMD ["sh", "/opt/tomcat/bin/catalina.sh", "jpda", "run"]
