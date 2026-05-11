## Install Java ON Windows:
* JDK is needed for maven, so install jdk
* [Refer Here](https://www.java.com/en/download/manual.jsp)
* For Maven Installtion
  * [Refer Here](https://maven.apache.org/download.cgi)
  * [3.8.3](https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.zip)

## Install Java, maven On Ubuntu
```bash
sudo apt update -y
apt install openjdk-17-jdk -y
# If any issuws wrt brken
apt --fix-broken install
cd /opt/
#wget https://dlcdn.apache.org/maven/maven-3/3.8.7/binaries/apache-maven-3.8.7-bin.tar.gz
wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
tar -xzvf apache-maven-3.8.8-bin.tar.gz
export PATH=$PATH:/opt/apache-maven-3.8.8/bin
mvn --version


# To make mvn avaialble after we exit also, do the following steps : for sudo only 
vi /etc/profile.d/maven.sh
export PATH=$PATH:/opt/apache-maven-3.8.7/bin
export M2_HOME=/opt/apache-maven-3.8.7
sudo chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh
```
## Install Openjdk 17, mvn 3.8.8 on Centos:
```bash
# https://techviewleo.com/install-java-openjdk-on-rocky-linux-centos/
# Install Openjdk 17
sudo yum -y install wget curl
wget https://download.java.net/java/GA/jdk17.0.2/dfd4a8d0985749f896bed50d7138ee7f/8/GPL/openjdk-17.0.2_linux-x64_bin.tar.gz
tar xvf openjdk-17.0.2_linux-x64_bin.tar.gz
sudo mv jdk-17.0.2/ /opt/jdk-17/
vim ~/.bashrc
  export JAVA_HOME=/opt/jdk-17
  export PATH=$PATH:$JAVA_HOME/bin
source ~/.bashrc
echo $JAVA_HOME
java --version

# Install Maven 3.8.8
cd /opt/
# wget https://dlcdn.apache.org/maven/maven-3/3.8.7/binaries/apache-maven-3.8.7-bin.tar.gz
wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
tar -xzvf apache-maven-3.8.8-bin.tar.gz
vi ~/.bashrc
  export PATH=$PATH:/opt/apache-maven-3.8.8/bin
  export M2_HOME=/opt/apache-maven-3.8.8
source ~/.bashrc
mvn --version

## Install nexus on ubutu

#configure java

apt install openjdk-17-jdk -y

#configure maven

wget https://download.java.net/java/GA/jdk17.0.2/dfd4a8d0985749f896bed50d7138ee7f/8/GPL/openjdk-17.0.2_linux-x64_bin.tar.gz
tar xvf openjdk-17.0.2_linux-x64_bin.tar.gz
sudo mv jdk-17.0.2/ /opt/jdk-17/

wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.9.15-bin.tar.gz
tar -xzvf apache-maven-3.9.15-bin.tar.gz


vi /etc/profile.d/maven.sh
export JAVA_HOME=/opt/jdk-17
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:/opt/apache-maven-3.9.15/bin
export M2_HOME=/opt/apache-maven-3.9.15


sudo chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh

#Install/configure nexus

# Download Nexus 
# TO get latest version use the below url
# https://help.sonatype.com/repomanager3/product-information/download/download-archives---repository-manager-3
wget https://download.sonatype.com/nexus/3/nexus-3.45.0-01-unix.tar.gz
tar -xzvf nexus-3.45.0-01-unix.tar.gz
mv nexus-3.45.0-01 /opt/nexus

# Create a nexus user.
# Nexus is not advised to run nexus service as a root user.
# So, we are creating a  user called nexus and grant sudo access to manage nexus services.
useradd nexus

#Give the sudo access to nexus user

visudo
nexus ALL=(ALL) NOPASSWD: ALL

#Change the owner and group permissions to /opt/nexus directory
chown -R nexus:nexus /opt/nexus
chmod -R 775 /opt/nexus
#Change the owner and group permissions to /opt/sonatype-work directory.
chown -R nexus:nexus /opt/sonatype-work
chmod -R 775 /opt/sonatype-work

#Open /opt/nexus/bin/nexus.rc file and  uncomment run_as_user parameter and set as nexus user.
vi /opt/nexus/bin/nexus.rc
run_as_user="nexus"

#Create nexus as a service
ln -s /opt/nexus/bin/nexus /etc/init.d/nexus

#Switch as a nexus user and start the nexus service as follows.
sudo su - nexus

#Enable the nexus services
sudo systemctl enable nexus

#Start the nexus service
sudo systemctl start nexus

# Access nexus repo



# For All Users
---------------------- 
vi /etc/profile
  export JAVA_HOME=/opt/jdk-17
  export PATH=$PATH:$JAVA_HOME/bin
  export PATH=$PATH:/opt/apache-maven-3.8.8/bin
  export M2_HOME=/opt/apache-maven-3.8.8

source /etc/profile
mvn --version
```

## Install Java 1.8 on Centos
### Oracle Java
```bash
#Login as a root user
sudo su -

##Change dir to /opt
cd /opt
yum install wget -y
wget -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
yum install jdk-8u131-linux-x64.rpm -y

java -version
```
