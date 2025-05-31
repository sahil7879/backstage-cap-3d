# Adding a Catalog
In this lab what we will be doing is adding a catalog  
for this we will be needing a github repo  
this repo can also be empty no problem we can add content later  
in this repo we will add a file that is necessary for backstage to create a catalog  
so create a file name catalog-info.yaml
add this content into your file 
for official documentation and more knowledge refer to this link - https://backstage.io/docs/features/software-catalog/
```
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: artist-web
  description: The place to be, for great artists
  labels:
    example.com/custom: custom_label_value
  annotations:
    example.com/service-discovery: artistweb
    circleci.com/project-slug: github/example-org/artist-website
  tags:
    - java
  links:
    - url: https://admin.example-org.com
      title: Admin Dashboard
      icon: dashboard
      type: admin-dashboard
spec:
  type: website
  lifecycle: production
  owner: artist-relations-team
  system: public-websites
```
after this step lets add this into our backstage lets go to our backstage app  
click on create on the left pannel  
on the top right corner it will ask for add existing component click on that  
it will open the page where it will ask for the url now keep in mind the url should be copied from the search bar and the location should be of catalog-info.yaml file 
it will look like this  
```
https://github.com/sahil7879/pythonflaskdemo/blob/main/catalog-info.yaml
```
 
then click on analyze and then import that repo and then view that component 

# Option 2  
we can also add catalog through code  
edit the file app.config.local.yaml and add this block  
target can be changed to your own repo catalog-info.yaml  

```
catalog:
  locations:
    - type: url
      target: https://github.com/backstage/backstage/blob/master/packages/catalog-model/examples/components/artist-lookup-component.yaml
```
we can also add multiple repo simultaneously by adding multiple 
```
- type: url
  target: https://github.com/backstage/backstage/blob/master/packages/catalog-model/examples/components/artist-lookup-component.yaml
```
