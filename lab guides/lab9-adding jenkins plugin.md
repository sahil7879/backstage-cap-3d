adding jenkins plugin  
create your server before adding into your jenkins  
use these commands to install jenkins  
```
sudo -i 
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get -y install jenkins

sudo apt update
sudo apt -y install fontconfig openjdk-21-jre

systemctl daemon-reload
systemctl restart jenkins 
systemctl status jenkins
```
 open in your browser using localhost:8080  
 now fetch initial password
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword 
```
install suggested plugins  
use that password to login  
create your login credential  
once on the homepage of jenkins create a job  
- new job
- add your name
- choose freestyle project
- add any description
- go to add build steps
- select execute shell
  add this in the box
  ```
  echo "hello how are you" >> test.txt
  cat test.txt
  ```
- save this pipeline
- select build and check builds

making our jenkins available outside localhost  
- go to dashboard
- click on mangae jenkins
- click on configure
- go to jenkins url and change it from localhost:8080 to ip:8080
making personal access token
- click on your avatar icon in top right corner
- go to security
- generate your pat token
  
  
now lets go to backstage configuration  
you can follow steps from this page    
what u need to do in frontend  
https://github.com/backstage/community-plugins/tree/main/workspaces/jenkins/plugins/jenkins  
what u need to do for backend  
https://github.com/backstage/community-plugins/tree/main/workspaces/jenkins/plugins/jenkins-backend  

