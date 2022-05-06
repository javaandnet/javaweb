FROM amazonlinux:2.0.20181114

RUN \
  rpm --import https://yum.corretto.aws/corretto.key && \
  curl -L -o /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo && \
  yum -y install java-1.8.0-amazon-corretto-devel

RUN \
  yum -y install wget && \
  yum -y install gzip && \
  yum -y install tar && \
  yum -y install maven

RUN \
  rm -rf /var/cache/yum/* && \
  yum clean all

RUN mvn package

