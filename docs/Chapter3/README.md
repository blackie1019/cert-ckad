# 

## ConfigMap

### Create ConfigMap

```yml
apiVersion: v1
kind: ConfigMap
metadata: 
  name: my-config-map
  namespace: ch-3-1
data:
  myKey: This is my Key
  anotherKey: This is another Key
```

### Use ConfigMap

#### Environment

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-with-config-map
  namespace: ch-3-1
spec:
  containers:
    - name: myapp-with-config-map
      image: busybox
      command: ['sh','-c', 'echo $(MY_VAR) && sleep 36000']
      env:
        - name: MY_VAR
          valueFrom:
            configMapKeyRef:
              name: my-config-map
              key: myKey
```

#### Mounted volume

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-with-config-map-v2
  namespace: ch-3-1
spec:
  containers:
    - name: myapp-with-config-map-v2
      image: busybox
      command: ['sh', '-c', 'echo $(cat /etc/config/anotherKey) && sleep 3600']
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: my-config-map
```

### How to check

```sh
kubectl logs {pod name}
```

---

## SecurityContexts

### Prerequisite

```sh
sudo -s
# Add user and group in k8s WorkNode
useradd -u 2000 container-user-0
useradd -u 2001 container-user-1
groupadd -g 3000 container-group-0
groupadd -g 3001 container-group-1

# Create file
mkdir -p /etc/message && echo "Hello, World!" | tee -a /etc/message/message.txt

# Change privilege to particular user and group
chown 2000:3000 /etc/message/message.txt
chmod 640 /etc/message/message.txt
```

### Create Pod with incorrect Permission

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-with-security-contexts
  namespace: ch-3-2
spec:
  securityContext:
      runAsUser: 2001
      fsGroup: 3001
  containers:
    - name: myapp-with-security-contexts
      image: busybox
      command: ['sh','-c','cat /message/message.txt && sleep 3600']
      volumeMounts:
        - name: message-volume
          mountPath: /message
  volumes:
    - name: message-volume
      hostPath:
        path: /etc/message
```

### Create Pod with correct Permission

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-with-security-contexts
  namespace: ch-3-2
spec:
  securityContext:
      runAsUser: 2000
      fsGroup: 3000
  containers:
    - name: myapp-with-security-contexts
      image: busybox
      command: ['sh','-c','cat /message/message.txt && sleep 3600']
      volumeMounts:
        - name: message-volume
          mountPath: /message
  volumes:
    - name: message-volume
      hostPath:
        path: /etc/message
```

### Check execute user and command in particular Pod

```sh
kubectl exec {pod name} -- ps
```

--- 

## Resource Requirements

- Resource request
  
  The amount of resources necessary to run a container.

  >*A pod will only be a run on a node that has enough available resources to run the pod's containers.*

- Resource limit

  A maximum value for the resource usage of a container.

Memory `is measured in bytes`. 64Mi means `64 Mebibytes`.

CPU `is measured in cores`. 250m means `250 milliCPUs, or 0.25 CPU ocres`.

### Create Pod with Resources Requirements

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-resource-pod
  namespace: ch-3-3
spec:
  containers:
    - name: myapp-container
      image: busybox
      command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "128Mi"
          cpu: "500m"
```

## References

- [Resource requests and limits of Pod and Container](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-requests-and-limits-of-pod-and-container)

---

## Secrets

`Secrets` are pieces of sensitive information stored in the kubernetes cluster, such as passwords, tokens, and keys.

```yml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
stringData:
  myKey: myPassword
```

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-secret-pod
spec:
  containers:
    - name: myapp-container
      image: busybox
      command: ['sh', '-c', "echo Hello, Kubernetes! && sleep 3600"]
      env:
        - name: MY_PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: myKey
```

## References

- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

---

## ServiceAccounts

https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/learn/f8825bca-109c-4536-8fd2-e62795257894/7f90eaf3-622f-49cc-af3d-b1c90a2df70c/watch

`ServiceAccounts` allow containers running in pods to access the kubernetes API. Some applications may need to interact with the cluster itself, and service accounts provide a way to let them do it securely, with properly limited permissions.

```sh
kubectl create serviceaccount my-serviceaccount -n ch-3-5
```

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-serviceaccount-pod
  namespace: ch-3-5
spec:
  serviceAccount: my-serviceaccount
  containers:
    - name: myapp-container
      image: busybox
      command: ['sh', '-c', 'echo hi && sleep 3600']
```

## References

- [Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

---

## Lab

```sh
kubectl create namespace lab-3
kubectl create serviceaccount candy-svc -n lab-3
```

- ConfigMap

```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: candy-service-config
  namespace: lab-3
data:
  candy.cfg: |-
    candy.peppermint-power: 100000000
    candy.nougat-armor-strength: 10
```

- Secret
  
```yml
apiVersion: v1
kind: Secret
metadata:
  name: db-password
  namespace: lab-3
stringData: 
  password: Kub3rn3t3sRul3s!
```

- Pod
  
```yml
apiVersion: v1
kind: Pod
metadata:
  name: candy-service
  namespace: lab-3
spec:
  serviceAccountName: candy-svc
  securityContext:
    fsGroup: 2000
  containers:
    - name: candy-service
      image: linuxacademycontent/candy-service:1
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "128Mi"
          cpu: "500m"
      volumeMounts:
        - mountPath: /etc/candy-service
          name: candy-service-volume
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-password
              key: password
  volumes:
    - name: candy-service-volume
      configMap:
        name: candy-service-config
```