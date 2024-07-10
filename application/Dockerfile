FROM ubuntu:24.04

# Install prerequisites
RUN apt-get -y update 
RUN apt-get -y install openjdk-21-jdk wget curl telnet vim inetutils-ping 
RUN mkdir /usr/local/tomcat
RUN wget https://downloads.apache.org/tomcat/tomcat-10/v10.1.25/bin/apache-tomcat-10.1.25.tar.gz -O /tmp/tomcat.tar.gz
RUN cd /tmp && tar xvfz /tmp/tomcat.tar.gz

RUN cp -Rv /tmp/apache-tomcat-10.1.25/* /usr/local/tomcat/

EXPOSE 8080
# java
ENV JAVA_HOME /usr/lib/jvm/java-21-openjdk-amd64

# Define default command.
CMD ["bash"]


WORKDIR /usr/local/tomcat/webapps

RUN curl -O -L https://github.com/bhaskarndas/sample-war/raw/main/sampletest.war


CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
