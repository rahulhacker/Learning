### Prerequisite:
  Install kubectl-- command line tool to connect to minikube cluster
  Install docker desktop

### Repository used to learn K8-- minikube provide you cluster, 
* Install minikube in your local https://minikube.sigs.k8s.io/docs/start/
for wimdows run through curl command
set up the path as provided in the docs, in case any error run through the powershell 
in admin mode

* Create the mongo username and password for mongo db using base64
## Command's to run
* minikube status -- might you get an error, run below command
* minikube start ---- start the different components running
* Output:
    minikube
    type: Control Plane
    host: Running
    kubelet: Running
    apiserver: Running
    kubeconfig: Configured

* kubectl get all
* kubectl get pod -o wide
* kubectl logs <pod-name>
* kubectl describe pod <pod-name>

# deploy the different components to run the web application
### Dependent file  should be deployed before the service dependent on those
* config file
* secret file
* mongo deployment
* web application

* kubectl apply -f mongo-config.yaml
* kubectl apply -f mongo-secret.yaml
* kubectl apply -f mongo.yaml--- db+service
* kubectl apply -f webapp.yaml---webapp+service--


### Get the node ip :
* kubectl get node-- output minikube--- 
* minikube ip

## deploy the different components to run the web application

### Application not running in the browser
* NAME                                    READY   STATUS    RESTARTS   AGE
* pod/mongo-deployment-855b879886-g9wm7   1/1     Running   0          71m
* pod/webapp-deployment-9fccd564d-ds8wl   1/1     Running   0          71m

* NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
* service/kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP          84m
* service/mongo-service     ClusterIP   10.101.230.101   <none>        27017/TCP        71m
* service/webapp-service    NodePort    10.101.43.167    <none>        3000:30100/TCP   71m

* NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
* deployment.apps/mongo-deployment    1/1     1            1           71m
* deployment.apps/webapp-deployment   1/1     1            1           71m

* NAME                                          DESIRED   CURRENT   READY   AGE
* replicaset.apps/mongo-deployment-855b879886   1         1         1       71m
* replicaset.apps/webapp-deployment-9fccd564d   1         1         1       71m


## Solution:

* Try out if it works:
* kubectl -n kube-system rollout restart deployment coredns

## 2nd solution:
* Minikube Ip automatically can't be accessed in localhost. Execute this command to tunnel it.
* minikube service <service-name> --url
* reference:https://minikube.sigs.k8s.io/docs/handbook/accessing/

* After creating tunnel, run below command
* minikube service webapp-service


|-----------|----------------|-------------|---------------------------|
| NAMESPACE |      NAME      | TARGET PORT |            URL            |
|-----------|----------------|-------------|---------------------------|
| default   | webapp-service |        3000 | http://192.168.49.2:30100 |
|-----------|----------------|-------------|---------------------------|
* Starting tunnel for service webapp-service.
|-----------|----------------|-------------|------------------------|
| NAMESPACE |      NAME      | TARGET PORT |          URL           |
|-----------|----------------|-------------|------------------------|
| default   | webapp-service |             | http://127.0.0.1:57804 |
|-----------|----------------|-------------|------------------------|
* Opening service default/webapp-service in default browser...
! Because you are using a Docker driver on windows, the terminal needs to be open to run it.




####
* NAME                                    READY   STATUS    RESTARTS   AGE
* pod/hello-minikube1-8587cd9b85-9rfkl    1/1     Running   0          51m
* pod/mongo-deployment-855b879886-g9wm7   1/1     Running   0          71m
* pod/webapp-deployment-9fccd564d-ds8wl   1/1     Running   0          71m

* NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
* service/hello-minikube1   NodePort    10.107.161.133   <none>        8080:32343/TCP   51m
* service/kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP          84m
* service/mongo-service     ClusterIP   10.101.230.101   <none>        27017/TCP        71m
* service/webapp-service    NodePort    10.101.43.167    <none>        3000:30100/TCP   71m

* NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
* deployment.apps/hello-minikube1     1/1     1            1           51m
* deployment.apps/mongo-deployment    1/1     1            1           71m
* deployment.apps/webapp-deployment   1/1     1            1           71m

* NAME                                          DESIRED   CURRENT   READY   AGE
* replicaset.apps/hello-minikube1-8587cd9b85    1         1         1       51m
* replicaset.apps/mongo-deployment-855b879886   1         1         1       71m
*replicaset.apps/webapp-deployment-9fccd564d   1         1         1       71m














