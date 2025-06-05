intallation minikube  
you can install minikube using root user but should run it outside of root  
```
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

minikube start
// you can check the instalation using this command 
```
installing kubectl
```
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
// you can check the instalation using this command 
```
  installing argo  
keep in mind that you are installing argocd in kubernetes using deployments  so install kubernetes first
```
kubectl create namespace argocd 
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
after installing we need to perform some steps to make our ui available 
```
kubectl get all -n argocd
kubectl edit service/argocd-server -n argocd
```

and do a change in the end of that file type: ClusterIP --> type: NodePort
save the file 
```
kubectl get svc -n argocd
```
fetch the nodeport that will be in this range 30000–32767
now use this command to fetch the node ip 
```
kubectl get nodes -o wide  

minikube service argocd-server -n argocd
```
and now check if it is opening or not in the browser 
node-ip:nodeport

to login  
fetch the password from kubernetes secret
```
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d && echo
```
username is admin and use the secret for the password

