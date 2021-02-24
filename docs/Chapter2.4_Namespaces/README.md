# Chapter 2.4 : Namespaces

## Namespaces

`Namespaces` provide a way to keep your objects organized within the cluster. Every object belongs to a namespace. When no namespace is specified, the cluster will assume the `default` namespace.

## Setting the namespace preference

You can permanently save the namespace for all subsequent kubectl commands in that context.

```sh
kubectl config set-context --current --namespace=<insert-namespace-name-here>
# Validate it
kubectl config view --minify | grep namespace:
```

## Lesson Reference

### Define Namespace

You can get a list of the namespaces in the cluster like this:

```sh
kubectl get namespaces
```

You can also create your own namespaces.

```sh
kubectl create ns my-ns

```

To assign an object to a custom namespace, simply specify its metadata.namespace attribute.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-ns-pod
  namespace: my-ns
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```

### Create resources under specific namespace

Create the pod with the created yaml file.

```sh
kubectl create -f my-ns.yml
```

Use the -n flag to specify a namespace when using commands like kubectl get .

```sh
kubectl get pods -n my-ns
```

You can also use -n to specify a namespace when using kubectl describe .

```sh
kubectl describe pod my-ns-pod -n my-ns
```

## References

- [Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/))