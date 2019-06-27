### Create a deployment

<details><summary>show</summary>
<p>



```YAML
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

</p>
</details>

#### Expose the deployment's replica pods with a service:

<details><summary>show</summary>
<p>



```YAML
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

</p>
</details>

### You can get more information about the service with these commands

<details><summary>show</summary>
<p>

```bash
kubectl get svc
kubectl get endpoints my-service
```
