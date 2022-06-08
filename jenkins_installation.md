# Install Jenkins on AWS EC2
Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

Jenkins is an open-source automation server that integrates with a number of AWS Services, such as AWS CodeCommit, AWS CodeDeploy, Amazon EC2 Spot, and Amazon EC2 Fleet. You can use Amazon Elastic Compute Cloud (Amazon EC2) to deploy a Jenkins application on AWS in a matter of minutes.

### In this tutorial, you will perform the following steps:
- Prerequisites

- Create a key pair using Amazon EC2 if you already have one, you can skip this step

- Install and configure Jenkins

### Prerequisites
1. An AWS account, if you don’t have one, you can register here https://aws.amazon.com/aispl/registration-confirmation/

2. An Amazon EC2 key pair
3.  EC2 Instance 
   - With Internet Access
   - Security Group with Port `8080` open for internet
4. Java 11 should be installed  

### Create a key pair
To create your key pair:

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/ and sign in.
2. In the navigation pane, under NETWORK & SECURITY, choose Key Pairs.
3. Select Create key pair.
4. For Name, enter a descriptive name for the key pair. Amazon EC2 associates the public key with the name that you specify as the key name. A key name can include up to 255 ASCII characters. It can’t include leading or trailing spaces.
5. For File format, choose the format in which to save the private key. To save the private key in a format that can be used with OpenSSH, choose pem. To save the private key in a format that can be used with PuTTY, choose ppk.
6. Select Create key pair.
7. The private key file is automatically downloaded by your browser. The base file name is the name you specified as the name of your key pair, and the file name extension is determined by the file format you chose. Save the private key file in a safe place.
8. If you will use an SSH client on a macOS or Linux computer to connect to your Linux instance, use the following command to set the permissions of your private key file so that only you can read it.


### Install and configure Jenkins
You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.
1. Get the latest version of jenkins from https://pkg.jenkins.io/redhat-stable/ and install

 - To ensure that your software packages are up to date on your instance, use the following command to perform a quick software update:

   ```sh
   $ sudo yum update 
   ```
 - Add the Jenkins repo using the following command:
   ```sh
   $ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   ```
 - Import a key file from Jenkins-CI to enable installation from the package:
   ```sh
   $ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
   ```
 - Install Java:
   ```sh
   $ sudo yum install java-1.8.0-openjdk-devel
   ```
 - Install Jenkins:
   ```sh
   $ sudo yum install jenkins
   ```
 - Enable the Jenkins service to start at boot:
   ```sh
   $ sudo systemctl enable jenkins
   ```
 - Start Jenkins as a service:  
   ```sh
   $ sudo systemctl start jenkins
   ```
 - You can check the status of the Jenkins service using the command:
   ```sh
   $ sudo systemctl status jenkins
   ```

## Accessing Jenkins
   By default jenkins runs at port 8080, You can access jenkins at
   
   ```sh
   http://YOUR-SERVER-PUBLIC-IP:8080
   ```
#### Configure Jenkins
- The default Username is `admin`
- Grab the default password 
- Password Location:`/var/lib/jenkins/secrets/initialAdminPassword`
- `Skip` Plugin Installation; _We can do it later_
- Change admin password
   - `Admin` > `Configure` > `Password`
- Configure `java` path
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK`  
- Create another admin user id   
