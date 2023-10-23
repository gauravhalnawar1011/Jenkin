Are you looking forward to learn Jenkins right from Zero(installation) to Hero(Build end to end pipelines)? then you are at the right place.
AWS Management Console -> 
AWS EC2 Instance
Go to AWS Console
Instances(running)
Launch instances
![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/b69a454d-6377-4e3f-adf9-5892768a704d)

Launch Instance -> Connect using Cloudshell/Mobaxterm/putty as per your Availability
Install Jenkins.

Pre-Requisites:

Java (JDK)
Run the below commands to install Java and Jenkins
Install Java

sudo apt update
sudo apt install openjdk-11-jre

Verify Java is Installed

java -version

Now, you can proceed with installing Jenkins

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

****Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.**

EC2 > Instances > Click on
In the bottom tabs -> Click on Security
Security groups
Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).

![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/f7f2e46b-3b6c-4a2f-bb19-b6c820bf25c2)

Login to Jenkins using the below URL:
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 
1. Delete the inbound traffic rule for your instance
2. 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins,
- Run the command to copy the Jenkins Admin Password -

- sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

- ![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/72ee252c-6dd6-4886-92ff-af9980c3eed9)

- ![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/a8102841-37ec-4dd2-9311-55e29ffae400)
 install suggested plugin

![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/89db1c0f-9c77-4a91-808b-4c82568ff73c)


Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/ddba93a1-53d0-4252-a2e9-2b1613ab7892)

**![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/1a5f276e-4dec-48bd-a86b-d5e0b0355205)
**

![image](https://github.com/gauravhalnawar1011/Jenkin/assets/140076717/8c1efb6c-f303-4fe7-8606-2bfbb7abcf75)

Wait for the Jenkins to be restarted.

Docker Slave Configuration
Run the below command to Install Docker

sudo apt update
sudo apt install docker.io
Grant Jenkins user and Ubuntu user permission to docker deamon.
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
Once you are done with the above steps, it is better to restart Jenkins.

http://<ec2-instance-public-ip>:8080/restart
The docker agent configuration is now successful.



