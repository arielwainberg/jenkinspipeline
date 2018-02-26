# maven-project
#Source code for James Lee's Jenkins course.
#
#Check out the full list of DevOps and Big Data courses that James and Tao teach.
#
#https://www.level-up.one/courses/

#This project used as Pratctice for Jenkins by Ariel Wainberg

The Solution:
Jenkins-pipeline-excerise:
The Jenkins file can be found on:

1. On Jenkins server:
a.	Generate SSH key in order to be able to connect to Jenkins to the other hosts:
	•	ssh-keygen –t rsa

b.	copy created private key to Jenkins user home folder (/var/lib/jenkins):
	•	cd ~
	•	cp ~/.ssh/rsa_id tomcat-demo.pem
	
2. On Production and staging Servers procedure the following steps:
	a.	Create “ec2user” in tomcat_prod and tomcat_dev server
		•	useradd –m ec2user –s /sbin/bash

	b.	to provide tomcat8 group permissions to the user ec2user
		•	usermod –G tomcat8 ec2user 

	c.	Create and add Jenkins server public key to the both Productions and Staging servers ec2user authotized_keys:
		•	sudo –I –u ec2user
		•	ssh-keygen –t rsa 
			(Just easy way to create the .ssh with the right permissions (make sure .ssh permission is 700)
		•	touch authorized_keys (make sure authorized_keys permission is 600)
		•	copy from Jenkins server the content of the file id_rsa.pub to the Production and Staging server authorized_keys
3.	On Jenkins server:

	a.	try the SSH connection from Jenkins server to Production and Staging server :
		•	sudo –i –u jenkins
		•	ssh ec2user@192.168.1.5) #productionIP
		•	ssh ec2user@192.168.1.6) #stagingIP
		-	In the first connection it should ask you to allow the fingerprint ( type “yes”)
		-	Make the connections again, and it should login the servers without prompting for password, that’s means      everything ok.
4.	Run the Job!


