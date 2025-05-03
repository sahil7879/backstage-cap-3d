# backstage-docs
hi in this document you will get all the details u will need to run the backstage app  
in here i will share some links from where u can get help if u get stuck  

- https://www.udemy.com/course/from-devops-to-platform-engineering-master-backstage-idps/learn/lecture/45907599#overview
- https://backstage.io/docs/overview/what-is-backstage

## some github links that are used in the project 
link for backstage app that u can clone where u want to run  
- https://github.com/sahil7879/backstage-app.git

 link for template  
- https://github.com/sahil7879/backstage-software-templates.git

link for the demo flask project  
- https://github.com/sahil7879/python-app.git

# some changes u will want to do before u run the project 

## Ready your github integration 

- you will need a github private token
- you will also need to create a github oauth app 

![ github oauth app Screenshot](images/screenshot1.png)

In this i have given ip address of my instance if u have cloned it locally  
Then use localhost instead of ip address  

save the three in a text file for further use 
```
GITHUB_CLIENT_ID
GITHUB_CLIENT_SECRET
GITHUB_TOKEN
```
## Now lets got to the place where you have cloned the backstage
Question do u have your nodejs installed ? if not install that
```
curl -fsSL https://deb.nodesource.com/setup_18.x -o nodesource_setup.sh
sudo -E bash nodesource_setup.sh
sudo apt-get install -y nodejs
npm install -g corepack
yarn set version stable
yarn install
```
First go to the directory of backstage 
```
cd backstage-app
```
Now make some changes in app.config.yaml file 
```
vi app.config.yaml
```
In app.config.yaml, change three urls there in which it has ip addresses to localhost with those same ports and everything u just need to change ips 

Before starting the app u will also need to start a container of postgres use this command 
``` bash
docker run -d \
  --name backstage-postgres \
  -e POSTGRES_USER=backstage \
  -e POSTGRES_PASSWORD=backstage \
  -e POSTGRES_DB=backstage \
  -p 5432:5432 \
  postgres:15
```
Next make changes in the users file for integration purposes 
```
vi catalog/entities/users.yaml
```
Change the name part to the username of your github
```
apiVersion: backstage.io/v1alpha1
kind: User
metadata:
  name: sahil7879
spec:
  memberOf: [developer]
```
and also set your environment variable 
```
export GITHUB_CLIENT_ID=xyz
export GITHUB_CLIENT_SECRET=xyz
export GITHUB_TOKEN=xyz
```
 make sure you are in backstage-app directory  
and start your backstage by using 
```
yarn start 
```
wait for line in the end  

webpack compiled successfully 

access your backstage app in your browser 
http://ip:3000
