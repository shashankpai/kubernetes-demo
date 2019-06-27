### Create a Pod 

<details><summary>show</summary>
<p>
  
```bash
vim my-pod.yml
```

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```

Create a pod from the yaml definition file:

```bash
kubectl create -f my-pod.yml
```

Edit a pod by updating the yaml definiton and re-applying it:

```bash
kubectl apply -f my-pod.yml
```
You can also edit a pod like this:

```bash
kubectl edit pod my-pod
```
You can delete a pod like this:

```bash
kubectl delete pod my-pod
```
</p>
</details>
