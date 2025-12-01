1️⃣ Deployment of index.html using EC2 (Docker + Nginx)
A. Launch EC2

Login → AWS Academy → Start Lab

EC2 → Launch Instance

AMI: Ubuntu (Free tier)

Arch: 64-bit

Instance: t2.micro

Key pair: Create new (.pem) → save

Network: Allow HTTP & HTTPS

Storage: 8 GB

Launch → Wait for 2/2 checks

Select instance → Connect

B. Connect via SSH (powershell - run as admin)
cd <path-to-pem>

ssh -i key.pem ubuntu@<Public-IP>

C. Install Required Software
sudo apt update
sudo apt install docker.io -y
sudo apt install git -y
sudo apt install nano -y

D. Create & Push index.html (Local System)
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin <github-url>
git push -u origin main

E. Clone Repo on EC2
git clone <github-url>
cd <repo-name>

F. Create Dockerfile
nano Dockerfile


Paste:

FROM nginx
COPY index.html /usr/share/nginx/html


Save → Ctrl+O Enter → Ctrl+X

G. Build & Run Docker
sudo docker build -t mywebapp .
sudo docker run -d -p 80:80 mywebapp

H. Access Application

Copy Public IPv4

Browser:

http://<Public-IP>

I. Stop & Cleanup
sudo docker ps
sudo docker stop <container-id>


EC2 → Terminate Instance

AWS Academy → End Lab

2️⃣ Maven Web Project Deployment in AWS
A. Launch EC2

Start Lab → EC2 → Launch Instance

Ubuntu + t2.micro

Create key pair

Allow all inbound

Wait for 2/2 checks

Connect → SSH

B. Connect & Install
sudo apt update
sudo apt install docker.io -y
sudo apt install git -y

C. Clone Maven Project
git clone <maven-github-url>
cd <project-folder>

D. If Branch Issue
git branch -M main


(or set default branch in GitHub → Settings)

E. Build Docker Image
sudo docker build -t mavenapp .

F. Run Container
sudo docker run -d -p 9090:8080 mavenapp

G. Open Port (If Not Loading)

EC2 → Security Groups → Edit Inbound Rules

Custom TCP | Port 9090 | 0.0.0.0/0

H. Access App
http://<Public-IP>:9090

I. Stop & Terminate
sudo docker ps
sudo docker stop <container-id>


Terminate EC2

End Lab

✅ REMEMBER

Use HTTP, not HTTPS

Always terminate instance

Always end lab


=====================================================================

MAVEN JAVA & MAVEN WEB PROJECT + PUSH TO GITHUB
🔹 A. Maven Java Project Creation (Quickstart)
Open Eclipse IDE (Enterprise Java & Web)
File → New → Maven Project
In Filter, type: quickstart
Select:
org.apache.maven.archetypes : maven-archetype-quickstart : 1.4
Click Next
Enter:
GroupId (TeamID): SE
ArtifactId: MavenJava
Click Next
Console asks → type Y → Enter
Project SE.MavenJava created with pom.xml
Open:
src/main/java → SE.MavenJava → App.java
Right click App.java → Run As → Maven Clean
                              → Maven Install
                              → Maven Test
                              → Maven Build
  In Goals, type:
clean install test
→ Apply → Run
16. Console shows BUILD SUCCESS
17. Right click App.java → Run As → Java Application
18. Output: Hello World
=========================================================
B. Maven Web Project Creation (WebApp)
Open Eclipse IDE
File → New → Maven Project
In Filter, type: webapp
Select:
org.apache.maven.archetypes : maven-archetype-webapp : 1.4
Click Next
Enter:
GroupId (TeamID): SE
ArtifactId: MavenWeb
Click Next
Console asks → type Y
Project SE.MavenWeb created with pom.xml
Open:
src/main/webapp → index.jsp
🔹 C. Add Servlet Dependency
Open browser → mvnrepository.com
Search Java Servlet API
Copy latest dependency
Paste into pom.xml (inside <dependencies>)
🔹 D. Configure Tomcat Server
Eclipse Menu → Window → Show View → Servers
Click No servers available
Select Tomcat v9.0 / v11.0
Click Next → Finish
Double-click Tomcat server (config page)
Select Use Tomcat Installation
Change ports:
Admin port → 0
HTTP/1.1 → 8085
Close tab
🔹 E. Tomcat Users Configuration
In Project Explorer → Servers
Open:
Apache Tomcat → conf → tomcat-users.xml
Paste above </tomcat-users>:

<role rolename="admin-gui,manager-gui,manager-script,manager-jmx,manager-status"/>
<user username="admin" password="1234" roles="manager-gui,admin-gui,manager-script"/>

Save & close
🔹 F. Build & Run Maven Web Project
Right click index.jsp → Run As → Maven Clean
                              → Maven Install
                              → Maven Test
                              → Maven Build
In Goals, type:
clean install test
→ Apply → Run
32. Console shows BUILD SUCCESS
33. Right click index.jsp → Run As → Run on Server
34. Choose existing Tomcat server → Finish
35. Output: Hello World Web Page
🔹 G. Push Maven Java Project to GitHub
Create GitHub repo for MavenJava
Eclipse → Right click MavenJava
Show in Local Terminal → Git Bash
git init
git branch -M main
git remote add origin <java-repo-url>
git add .
git commit -m "Maven Java push"
git push -u origin main
🔹 H. Push Maven Web Project to GitHub
Create GitHub repo for MavenWeb
Eclipse → Right click MavenWeb
Show in Local Terminal → Git Bash
git init
git branch -M main
git remote add origin <web-repo-url>
git add .
git commit -m "Maven Web push"
git push -u origin main
