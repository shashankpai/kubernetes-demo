### get all the namespaces on a cluster 

<details><summary>show</summary>
<p>

```bash
kubectl get ns --show-labels
```

</p>
</details>

### Create a namespace called 'dev','prod' and 'qa' and a pod with image nginx in each namespace

<details><summary>show</summary>
<p>

```bash
kubectl create namespace prod
kubectl create namespace qa
kubectl create namespace dev
kubectl run nginx --image=nginx --restart=Never -n prod
kubectl run nginx --image=nginx --restart=Never -n dev
kubectl run nginx --image=nginx --restart=Never -n qa
```

</p>
</details>

### Create a namespace using yaml named 'dev'

<details><summary>show</summary>
<p>


```yaml
apiVersion: v1
kind: Namespace
metadata: 
  name: dev
```

</p>
</details>

### Create a nginx pod  using yaml in  'dev' namespace

<details><summary>show</summary>
<p>

```bash
vim nginx-dev.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  restartPolicy: Never
```

```bash
kubectl create -f nginx-dev.yaml -n dev
```

</p>
</details>

### Get pods from all namespaces 

<details><summary>show</summary>
<p>

```bash
kubectl get pods --all-namespaces
```
</p>
</details>

### Get pods for a specific  namespace example dev 

<details><summary>show</summary>
<p>

```bash
kubectl get pods -n dev
```
</p>
</details>

### Locate pods by node 

<details><summary>show</summary>
<p>

```bash
kubectl get pods -n dev -o wide 
```
</p>
</details>




