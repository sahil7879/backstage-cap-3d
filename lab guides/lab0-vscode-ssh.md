# VSCode SSH
if the user want they can also ssh via vscode and it will be easier to navigate in the folder and do changes in the file  
## NOTE THIS WILL ONLY BE ABLE TO GIVE ACCESS TO UBUNTU/ANY OTHER USER AND NOT ROOT USER  
for this open vs code  
add extension -> remote-ssh extension  
than go to search bar and click on run commands  
search for remote-ssh - connect to host  
add new ssh host  
add the connect command that will look like this  
```
ssh -i "key.pem" ubuntu@public-ip
```
is the user want to connect with the password just use this 
```
ssh ubuntu@public-ip
```
then it will ask for pasword then paste the password

after that u will be able to open folder in that vm 
