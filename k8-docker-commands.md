https://docs.docker.com/engine/docker-overview/
https://docs.docker.com/install/


Docker Commands 101
docker run --detach --name web nginx:latest
wget -O - http://web:80/
docker logs web
docker stop web

docker run -d --name bb1 busybox:latest /bin/sh -c "sleep 30000"
docker exec bb1 ps docker exec command to run additional processes in a running container
docker create nginx 

docker run -d --name wpdb -e MYSQL_ROOT_PASSWORD=ch2demo mysql:5
docker run -d --name wp2 --link wpdb:mysql -p 80 --read-only wordpress:4

docker run --env MY_ENVIRONMENT_VAR="this is a test" busybox:latest env ( injecting environment variable)
docker ps -a (list all containers)

Packaging software in Images
 


Kubernetes 101
kubectl expose deployment tomcat-deployment --type=NodePort
 
minikube ssh use/password docker:tcuser

minikube start
kubectl get pods -n kube-system
minikube dashboard



kubectl apply -f deployment.yaml
kubectl expose deployment tomcat-deployment --type=NodePort
minikube service tomcat-deployment --url
kubectl get pods

cheatsheet
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
https://github.com/ramitsurana/awesome-kubernetes
https://github.com/kubernauts/Kubernetes-Learning-Resources/blob/master/pages/books.md
https://kubernetes.io/docs/tutorials/

Commands For Cut & Paste
kubectl get pods
kubectl get pods [pod name]
kubectl expose <type name> <identifier/name> [—port=external port] [—target-port=container-port [—type=service-type]
kubectl port-forward <pod name> [LOCAL_PORT:]REMOTE_PORT]
kubectl attach <pod name> -c <container>
kubectl exec  [-it] <pod name> [-c CONTAINER] — COMMAND [args…]
kubectl label [—overwrite] <type> KEY_1=VAL_1 ….
kubectl run <name> —image=image

#Create load-balancer service
kubectl apply -f deployment.yml
kubectl expose deployment tomcat-deployment --type=NodePort (or)
kubectl expose deployment tomcat-deployment --type=LoadBalancer --port=8080 --target-port=8080 --name=tomat-load-balancer
kubectl describe services tomcat-load-balancer
minikube service tomcat-load-balancer --url
kubectl scale —replicas=4 deployment/tomcat-deployment


#rollout and deployment
kubectl get deployments
kubectl rollout status deployment tomcat-deployment
kubectl set image deployment/tomcat-deployment tomcat=tomcat:9.0.1
kubectl rollout history deployment/tomcat-deployment --revision=2
kubectl describe deployment tomcat-deployment

#dashboard
kubectl proxy ( access k8 dashboard url)
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml ( create dashboard )

#delete minikube
kubectl delete deployment tomcat-deployment
* To ensure you are starting with a clean slate: `minikube delete; sudo rm -rf ~/.minikube; sudo rm -rf ~/.kube`


