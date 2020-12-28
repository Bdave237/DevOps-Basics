#  Install & configure Maven build tool on Jenkins
Maven is a code build tool which used to convert your code to an artifact. this is a widely used plugin to build in continuous integration


#### Prerequisites
1. Jenkins server

#### Install Maven on Jenkins
1. Install Apache Maven on your EC2 instance. First, enter the following to add a repository with a Maven package
  
     # downloading maven from Fedora Repository
     
     	sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
     
	
2. Enter the following to set the version number for the packages.

	sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
	
3. Then you can use yum to install Maven.

	sudo yum install -y apache-maven
4. The Gremlin libraries require Java 8

Make sure you install java 8 on your Jenkins Server.

#### Checkpoint 
1. logoff and login to check maven version
  
Run the following command to check version of Maven installed.
    mvn --version
    ```
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps. 

### Setup maven on Jenkins console
1. Install maven plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

2. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`
