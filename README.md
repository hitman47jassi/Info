# Info
Learning info
SERVER SETUP
JENKINS
GITS
ECLIPSE


----------------------------SERVER Setup------------------------------------------------------------------------------------
	Create EC2 instance
	Remember to generate PEM file.
	You can edit it anytime. Name to XYZ server


----------------------------Putty Setup------------------------------------------------------------------------------------
	https://www.youtube.com/watch?v=bi7ow5NGC-U&ab_channel=LinuxAcademy

	1. Download putty.exe
	2. Download puttygen.exe

	Pre-requisite:
	AWS account 
	AWS EC2 server up and running.
	- Generate PEM file and download it to your system.
	- PEM file will help you to generate PPK file for authentication

	START:
	Open puttygen.exe
	Load >> select PEM file >> Click on Private key >> select path to save PPK >> done.

	Open putty.exe
	Connection>> SSH >> Auth >> Browse PPK.
	Session >> Hostname(Public IPv4 address) >> SAVE >> Open.

	USERNAME bydefault for AWS is : ec2-user 


----------------------------Java Installation--------------------------------------------------------
	https://www.youtube.com/watch?v=c_nF2RnyfDU&ab_channel=BhargavAmin

	Once putty is connected successfully then install Java

	Sudo su-
	yum install java-1.8*

	-Once java is installed successfully, now its time to set the java path in .bash_profile (got to root by sudo su and do ls -la)
	Putty java path is: "/usr/lib/jvm"
	If any issue switch to sudo su
	Copy this file name "java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64" This may differ if java version is different.
	So Create below java home path
	
	
	or 
	
	Search: readlink -f $(which java)
	Remove: /bin/java -- from the link and use.
	
	JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64/jre"
	JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64/jre"

	


	{{{#example----------
		PATH=$PATH:$HOME/.local/bin:$HOME/bin

		# java env Variable
		JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64/jre"

		PATH=$JAVA_HOME/bin:$PATH

		echo "Hi jassi, lets learn jenkins"
		export PATH
	}}}


	RESTART putty and do sudo su >> echo $PATH.
	you should be able to see path is udpated with java in it.
	If java path is not available then big problem-



----------------------------WGET Installation------------------------------------------------------------------------------------
	We need wget to be in server to install jenkins.
	sudo su
	yum install wget

	if already installed then you will see this msg: "Package wget-1.14-18.amzn2.1.x86_64 already installed and latest version"


----------------------------Jenkins Installation------------------------------------------------------------------------------------
	https://www.youtube.com/watch?v=jmm8DsosBqw&ab_channel=AutomationStepbyStep-RaghavPal

	Commands:
	sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
	sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
	sudo yum upgrade
	sudo yum install jenkins java-1.8.0-openjdk-devel
	sudo systemctl daemon-reload

----------------------------Start Jenkins------------------------------------------------------------------------------------
	Open Putty>
	sudo systemctl start jenkins
					sudo service jenkins start

	Check status>> sudo systemctl status jenkins



----------------------------Access Jenkins via Browser------------------------------------------------------------------------------------
jassi/L@123
	http://{ec2-public-dns}:8080
	---Working---
	http://18.222.176.119:8080/
Password file: cat /var/lib/jenkins/secrets/initialAdminPassword
	Initian admin passwrod ()
	941370e5330a4dd2b8b1c74e94c1fad1

	To fetch initial admin password
	sudo su -
	cd /var/lib/jenkins/secrets/
	cat initialAdminPassword
	0bcbbcab7f984af7b4171b55e9201d04
	To stop Jenkins
	sudo service jenkins stop

----------------------------uninstall Jenkins------------------------------------------------------------------------------------
	To uninstall Jenkins
	 sudo service jenkins stop
	 sudo yum remove jenkins
	 sudo rm -r /var/lib/jenkins
	 
	 
----------------------------Install Git in Jenkins------------------------------------------------------------------------------------
	https://cloudaffaire.com/how-to-install-git-in-aws-ec2-instance/
	sudo yum update -y
	sudo yum install git -y
	 
	 
	 
	 
	 





GIT------------------------------------------------------------------------------------
https://www.youtube.com/watch?v=LPT7v69guVY&ab_channel=AutomationStepbyStep-RaghavPal


** How to add eclipse java project to GIT HUB**
1. Create Accout in GITHUB
	Start project
	Create Repository
2. Start eclipse
	Open Perspective
	Select GIT
3. Create New project >> right click >> Team >> Share >> Configure Git repository
	Dropdown repository select your GIT repository >> Finish
4. Commit:
	Right click on project >> Team >> Commit.
	Open staging view
	Comit with comment
5. If Github desktop is available then check code.. and hit Publish repository.
	Check online github files are uploaded
	

GIT integration to Jenkins------------------------------------------------------------------------------------
**How to configure git plugins in jenkins**
1. Open Jenkins >> Manage jenkins>> Manage Plugins >> Available >> Github integration plugin check box check.
	Install and restart.

2. Dashboard >> New Items Search testing







ISSUE FACED:

1. jenkins	
	1. Make sure git is installed in jenkins server
	2. Make sure Required plugin is installed in jenkins
	
If Git repository path is throwing error then check Jenkins >> Manage Jenkkins >> Global tool configuration >> Git >> Path to Git executable section: "/usr/bin/git"
You can check your path by using "Whereis git" command in putty jenkins server if installed.



2. Issue I faced for 3 days.. 
	Jenkins Pipeline is not picking Jenkinsfile from git.
	Solution : In Git hub your Jenkinsfile should be in master main directory.. not in sub directory.
	
	Checkout this link
	https://stackoverflow.com/questions/46277936/run-jenkins-pipeline-with-code-from-git/54670376












