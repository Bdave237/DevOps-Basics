#  Install & configure Maven build tool on Jenkins
Maven is a code build tool which used to convert your code to an artifact. this is a widely used plugin to build in continuous integration


#### Prerequisites
1. Jenkins server

#### Install Maven on Jenkins
For this installation, we will use/opt/maven as our installation PATH

1. log into your ec2 instance, elevate to root user  and cd into /opt directory.
	 sudo su
	cd /opt

2. Install Apache Maven on your EC2 instance. Go to Maven website and copy link to download maven (https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz)
  
# downloading maven into your /opt directory. run bellow command
     
     	sudo wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
     
	
3. run the following command to extract maven binaries into your /opt directory.

	 tar -xxvf apache-maven-3.6.3-bin.tar.gz
	
4. Copy maven binaries into /opt/maven directory by running below command

	 mv apache-maven-3.6.3-bin.tar.gz maven

	
5. The Gremlin libraries require Java 8

Make sure you install java 8 on your Jenkins Server.

6. Make sure you add your Maven home into your PATH by editing .bashrc in root home directory. run following commands to edit .bashrc

	cd 
	
	vi .bashrc
    
   add following line at end of your .bashrc file
   	
	PATH=/opt/maven/bin:$PATH
	
    run the following command to make new changes in .bashrc effective
    
	./.bashrc

#### Checkpoint 
7. logoff and login to check maven version
  
Run the following command to check version of Maven installed.
   	 mvn --version
 
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps. 

### Setup maven on Jenkins console
8. Install maven plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

9. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`
