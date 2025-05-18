# postgre server integretion
Right now we have sqllite for the backend and that is in memory db so it will give us problem if we restart our backstage  
Now we need to change it to postgre so it will be non volatile  
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

```
