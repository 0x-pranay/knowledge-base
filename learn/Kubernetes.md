```
## add cluster config
aws eks update-kubeconfig --region ap-south-1 --name xx-aps1-eks-cluster

```

##### List all namespaces

`kubectl get namespaces`

##### Get current cluster

`kubectl config current-context`

#### Set default namespace for that context

`kubectl config set-context --current --namespace=<your-namespace>`

#### show current namespace

`kubectl config view --minify | grep namespace`

##### list all deployments

`kubectl get deployments -n <namespace>`

#### list all pods

`kubectl get pods`

##### restart

`kubectl rollout restart deployment <your-deployment-name> -n <namespace>`

#### Show deployment

`kubectl get deployment -n <namespace>`

`kubectl describe deployment <deployment-name> -n <namespace>`

###### update the deployment with new image tag

```
kubectl set image deployment/<deployment-name> <container-name>=<ecr-repo-uri>:0.0.3 -n <namespace>
```

#### rollout status

```
kubectl rollout status deployment/<deployment-name> -n <namespace>
```

#### restart

```
kubectl rollout restart deployment/<deployment-name> -n <namespace>
```

##### copy a file into a container

`kubectl cp localfile.js <pod-name>:/app/localfile.js -n your-namespace`

```


```

### Logs

##### View logs of a specific pod

```
kubectl logs <pod-name> -n <namespace>
```

#### tail logs

`kubectl logs -f <pod-name> -n <namespace>`

#### view logs of a crashed container

`kubectl logs <pod-name> --previous -n <namespace>`
