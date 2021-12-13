# Setting up Jenkins server and using it

## Task
- You will be sharing your Jenkins servers
- Research how to setup a Jenkins server
- Create a server instance per group on EC2. Label it in the following format. name-name-name-Jenkins
- Setup Jenkins to run on your instance
- Create user accounts for each user on Jenkins and restrict access to logged in users only
- Build multi stage CICD pipeline with CI, Testing, CD and CDE
- Deploy it in your own VPC - public and private subnets for app private for db
- Aim is to see all three pages working - home page - Fibonacci/4 - /posts

## Diagrams
### Overview 

![image](https://user-images.githubusercontent.com/94615905/145805744-590675a2-559e-4c71-ad01-99d5b746e722.png)

### AWS

![image](https://user-images.githubusercontent.com/94615905/145810930-7b12a304-01fd-4a39-b480-126c08c6f365.png)

## Creating Jenkins server

> To use Jenkins Java needs to be installed
- Step 1: Create an ec2 instance for jenkins
- Step 2: Install Java

```
sudo apt update
sudo apt install openjdk-11-jdk
```
 > `sudo apt search openjdk` can be used to see what JDK are available. The code above installs JDK 11

`java -version` to check the installation 

- Step 3: Install jenkins on ec2 instance

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt install jenkins
```

> link to usefull doc to help install jenkins (https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04) 


