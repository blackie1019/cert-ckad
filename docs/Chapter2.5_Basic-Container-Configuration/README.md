# Chapter 2.5 : Basic Container Configuration

https://acloudguru-content-attachment-production.s3-accelerate.amazonaws.com/1597954870857-01_05_Basic%20Container%20Configuration.pdf

## Lesson Learn

You can specify custom commands for your containers.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-command-pod
  labels:
    app: myapp
spec:
  containers:
    - name: myapp-container
      image: busybox
      command: ['echo']
      restartPolicy: Never
```

You can also add custom arguments like so:

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-args-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['echo']
    args: ['This is my custom argument']
  restartPolicy: Never
```

Here is a pod with a containerPort:

```yml
apiVersion: v1
kind: Pod
metadata:
  name: my-containerport-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: nginx
    ports:
    - containerPort: 80
```

## References

- [Define a Command and Arguments for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)