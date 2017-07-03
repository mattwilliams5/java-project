# java-project

For this project you will need a Jenkins Master and Slave both with docker installed on Centos7 and ant

# Set up environment

# Java install 

wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
rpm -Uvh jdk-8u131-linux-x64.rpm
alternatives --install /usr/bin/java java /usr/java/latest/bin/java
alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000


# Jenkins install

wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install -y jenkins-2.19.4-1.1
systemctl start jenkins
systemctl enable jenkins
watch n=1 "netstat -tulpn|grep 8080"


# Docker install

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum clean all
yum install docker-ce-17.03.0.ce-1.el7.centos
yum install  docker-ce-selinux-17.03.2.ce-1.el7.centos
gpasswd -a jenkins docker
systemctl restart jenkins


# Ant install

wget http://www.us.apache.org/dist/ant/binaries/apache-ant-1.10.1-bin.tar.gz
tar xvfvz apache-ant-1.10.1-bin.tar.gz -C /opt
ln -s /opt/apache-ant-1.10.1/ /opt/ant
ln -s /opt/ant/bin/ant /usr/bin/ant




