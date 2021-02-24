# Chapter 2.3 : Creating Pods

https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/learn/638c1a6b-7159-4c72-968c-7b13c2232da3/c0a4e950-41d2-4f8d-9417-a3456ade999a/watch

## Pods

`Pods` are the basic building blocks of any application running in kubernetes.

## Command

my-pod.yml

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: ct-app
spec:
  containers:
  - name: ct-app-container
    image: busybox
    command: ['sh','-c','echo Hello CT!&&sleep3600']
```

### Create

```sh
kubectl create -f my-pod.yml # 建立 Pod
kubectl get pods # 確認 Pod
```

### Modify

```sh
kubectl apply -f my-pod.yml # 修改 Pod, by .yml
## 或是

kubectl edit pod my-pod
```

### Delete

```sh
kubectl delete pod my-pod
```
