# lab2-creating-backstage
### Step 1
If we are still root then do exit 
```
exit
```
### Step 2
now lets create a folder in this user 
```
mkdir backstage-app && cd backstage-app
```
### Step 3
run this command to create our own backstage app
```
npx @backstage/create-app@latest
```
after this command it will ask for confirmation and the name of our app type y for confirmation and after that input the name of your app that we want to give 
### Step 4
get into your app that you have created 
```
cd your-app-name
```
### Step 5
now lets start our backstage app 
```
yarn start
```
you will be able to access backstage base app on your localhost:3000 in your web browser
### step 6
if you are working with a cloud vm then you will have to make some changes in app.config.yaml file 
```
vi app.config.yaml
```
do these changes  
-- under app:
- in baseurl change localhost to your vms public ip 
- under base url add this block 
```
  listen:
    host: 0.0.0.0
```
-- under backend:
- same as in app in here too change baseurl localhost --> public ip of vm
- under baseurl in listen uncomment host and change it to 0.0.0.0
- the whole file should look something like this
```
app:
  title: Scaffolded Backstage App
  baseUrl: http://40.192.33.246:3000
  listen:
    host: 0.0.0.0
organization:
  name: My Company

backend:
  # Used for enabling authentication, secret is shared by all backend plugins
  # See https://backstage.io/docs/auth/service-to-service-auth for
  # information on the format
  # auth:
  #   keys:
  #     - secret: ${BACKEND_SECRET}
  baseUrl: http://40.192.33.246:7007
  listen:
    port: 7007
    # Uncomment the following host directive to bind to specific interfaces
      host: 0.0.0.0
```
