# Let's create k8s deployment with helm chart !!! 


First Create a helm chart. 
```
helm create chart 
after that, we can see the following list
root@k8s:/home/angel/angel-chart# ls -al
total 28
drwxr-xr-x 4 root root 4096 Nov  4 17:40 .
drwxr-xr-x 3 root root 4096 Nov  4 17:40 ..
-rw-r--r-- 1 root root  349 Nov  4 17:40 .helmignore
-rw-r--r-- 1 root root 1147 Nov  4 17:40 Chart.yaml
drwxr-xr-x 2 root root 4096 Nov  4 17:40 charts
drwxr-xr-x 3 root root 4096 Nov  4 17:40 templates
-rw-r--r-- 1 root root 1878 Nov  4 17:40 values.yaml
```

Let's remove everything from the chart first. 
```
 rm -rf angel-chart/templates/*.*
```

After that, update helm template files: 
```
kubectl create deployment ubuntu-test --image=ubuntu --dry-run=client -o yaml > deployment.yaml
```
service.yaml file here: 
```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: ubuntu
  name: ubuntu
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: ubuntu
  type: NodePort
```
$ helm list
$ helm install ubuntu angel-chart
```


Update values.yaml file first, 
```
image:
  name: ubuntu
  repository: ubuntu
  pullPolicy: IfNotPresent
  tag: "1.20"
```

After that, update both deployment and service yaml files: 
Update the template/deployment.yml file with https://github.com/Angelszm/helm-labs/blob/main/angel-chart/templates/deployment.yaml


Update the template/service.yml file with https://github.com/Angelszm/helm-labs/blob/main/angel-chart/templates/service.yaml
Also, don't forget to add helper file. 


Then, update values file with https://github.com/Angelszm/helm-labs/blob/main/angel-chart/values.yaml


```
$ helm list
$ helm install ubuntu2 angel-chart
```

```
root@k8s:/home/angel# helm list
NAME   	NAMESPACE	REVISION	UPDATED                                	STATUS  	CHART            	APP VERSION
ubuntu 	default  	1       	2022-11-04 17:50:29.373085125 +0000 UTC	deployed	angel-chart-0.1.0	1.16.0
ubuntu2	default  	1       	2022-11-04 18:15:01.335501569 +0000 UTC	deployed	angel-chart-0.1.0	1.16.0
- 

