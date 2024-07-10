#Base Image
FROM ubuntu:18.04

#Update APT repository & Install gnupg
RUN apt-get update && apt-get install -y gnupg wget telnet 

#Add an account for running MySQL
RUN groupadd -r mysql && useradd -r -g mysql mysql

RUN wget -qO - https://repo.mysql.com/RPM-GPG-KEY-mysql-2023 | apt-key add -

#Add the MySQL APT repository & Install necessary programs
RUN apt-get update \
    && echo "deb http://repo.mysql.com/apt/ubuntu/ bionic mysql-5.7" > \
      /etc/apt/sources.list.d/mysql.list \
    && apt-key adv --keyserver pgp.mit.edu --recv-keys 5072E1F5 \
    && apt-get update \
    && apt-get install -y --no-install-recommends perl pwgen

#Install MySQL
    #Set MySQL root password for silent installation
RUN ( echo mysql-community-server mysql-community-server/root-pass password ''; \
    echo mysql-community-server mysql-community-server/re-root-poss password ''; ) | debconf-set-selections \
    && apt-get install -y mysql-server \
    && mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
    && chmod 777 /var/run/mysqld

#Solve the problem that ubuntu cannot log in from another container
RUN sed -i 's/bind-address/#bind-address/' /etc/mysql/mysql.conf.d/mysqld.cnf

#Mount Data Volume
VOLUME /var/lib/mysql

#Expose the default port
EXPOSE 3306

#Start MySQL
CMD ["mysqld","--user","mysql"]
