### create a pod with labels environment: production

<details><summary>show</summary>
<p>

```bash
vim my-production-label-pod.yaml
```

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: my-production-label-pod
  labels:
    app: my-app
    environment: production
spec:
  containers:
  - name: nginx
    image: nginx
```

```bash
kubectl create -f my-production-label-pod
```

</p>
</details>


### create a pod with labels environment: development

<details><summary>show</summary>
<p>

```bash
vim my-development-label-pod.yaml
```

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: my-development-label-pod
  labels:
    app: my-app
    environment: development
spec:
  containers:
  - name: nginx
    image: nginx
```

```bash
kubectl create -f my-development-label-pod.yaml
```

</p>
</details>

### use various selectors to select different subsets of objects

<details><summary>show</summary>
<p>

```bash
kubectl get pod -l environment=development
kubectl get pod -l environment=production
kubectl get pods -l environment!=production

kubectl get pods -l 'environment in (development,production)'

kubectl get pods -l app=my-app,environment=production
```

</p>
</details>

### label a node using kubectl 

<details><summary>show</summary>
<p>

```bash
kubectl label node <node_name> accelerator=nvidia-tesla-p100
```

</p>
</details>

### Create a pod that will be deployed to a Node that has the label 'accelerator=nvidia-tesla-p100'

<details><summary>show</summary>
<p>

We can use the 'nodeSelector' property on the Pod YAML:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
  nodeSelector: # add this
    accelerator: nvidia-tesla-p100 # the slection label
```

You can easily find out where in the YAML it should be placed by:

```bash
kubectl explain po.spec
```

</p>
</details>
