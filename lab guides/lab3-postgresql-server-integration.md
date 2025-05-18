# postgre server integretion
Right now we have SQLite for the backend and that is in-memory db so it will lose all data on restart    
Now we need to change it to PostgreSQL so it will be persistent  
For that what we can do, we can start a container for the db  
But first we will give our user access to use docker so that we do not change our user again and again  
```
sudo usermod -aG docker ubuntu
```
now exit the ssh and ssh again  
and then try docker command to check whether it is working for ubuntu user  
```
# command to check docker 
docker ps
```
now lets add our postgre container 
```
docker run -d \
  --name backstage-postgres \
  --restart always \
  -e POSTGRES_USER=backstage \
  -e POSTGRES_PASSWORD=backstage \
  -e POSTGRES_DB=backstage \
  -p 5432:5432 \
  postgres:15
```
now lets check whether our container is running with the same command 
```
docker ps 
```
now lets integrate it into our backstage  
now if you go to our backstage directory there you will see app.config.local.yaml file lets edit that file 
```
vi app.config.local.yaml
```
add this block for integration 
```
backend:
  database:
    client: pg
    connection:
      host: localhost
      port: 5432
      user: backstage
      password: backstage
      database: backstage
```
this block will make sure you are connected to postgre container 
