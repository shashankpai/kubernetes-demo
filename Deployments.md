# Deployments

### create a sample nginx deployment with 3 replicas 

<details><summary>show</summary>
<p>

```bash
vim nginx-deployment.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
 ```
 
 ```bash
 kubectl create -f nginx-deployment.yaml
 ```
 
 </p>
</details>

### Get the deployments on cluster using kubectl

<details><summary>show</summary>
<p>

```bash
kubectl get deployments
```

</p>
</details>

### Get the deployments with deployment-name using kubectl

<details><summary>show</summary>
<p>

```bash
kubectl get deployments nginx-deployment
```

</p>
</details>

### Describe the deployment using kubectl 

<details><summary>show</summary>
<p>

```bash
kubectl describe deployment nginx-deployment
```

</p>
</details>

### Delete the deployment using kubectl 

<details><summary>show</summary>
<p>

```bash
kubectl delete deployment nginx-deployment
```

</p>
</details>

###  sample nginx deployment to practice rolling updates and rollback 

<details><summary>show</summary>
<p>

```bash
vim nginx-deployment-roll.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rolling-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.1
        ports:
        - containerPort: 80
 ```
 
 ```bash
 kubectl create -f nginx-deployment-roll.yaml
 ```
 
 </p>
</details>

 ### Perform a rolling update  

<details><summary>show</summary>
<p>

```bash
kubectl set image deployment/rolling-deployment nginx=nginx:1.7.9 --record
```

</p>
</details>


### Explore the rollout history of the deployment.

<details><summary>show</summary>
<p>

```bash
kubectl rollout history deployment/rolling-deployment

kubectl rollout history deployment/rolling-deployment --revision=2
```

</p>
</details>

### roll back to the previous revision like so

<details><summary>show</summary>
<p>

```bash
kubectl rollout undo deployment/rolling-deployment
```

</p>
</details>

 ### You can also roll back to a specific earlier revision by providing the revision number
 
 <details><summary>show</summary>
<p>

```bash
kubectl rollout undo deployment/rolling-deployment --to-revision=1
```

</p>
</details>


### control how rolling updates are performed by setting maxSurge and maxUnavailable in the deployment spec:

<details><summary>show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rolling-deployment
spec:
  strategy:
    rollingUpdate:
      maxSurge: 3
      maxUnavailable: 2
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.1
        ports:
        - containerPort: 80
```

</p>
</details>
