# Chapter 2.2 : Kubernetes API Primitives

https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/learn/638c1a6b-7159-4c72-968c-7b13c2232da3/b86ec97f-f2e8-4a8b-b969-4249553ff582/watch

## API Primitives

Kubernetes Object = Kubernetes API Primitives

- Pod
- Node
- Service
- ServiceAccount

`kubectl api-resources` 可以條列物件

e.g.

```sh
kubectl api-resources -o name
```

- Spec
  
  > For objects that have a spec, you have to set this when you create the object, providing a description of the characteristics you want the resource to have: its desired state.
  提供需要的規格

- Status

  >The status describes the current state of the object, supplied and updated by the Kubernetes system and its components. The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied.
  當前物件的狀態

顯示物件資訊
```
kubectl describe $object_type $object_name
```

e.g.

```sh
kubectl get pods -n kube-system # 使用預設於 kube-system 背景執行的 Pods

kubectl describe $object_type $object_name -o yaml # 透過 yaml 格式顯示該物件所有屬性
```

## Lesson Reference

```sh
kubectl api-resources -o name
kubectl get pods -n kube-system
kubectl get nodes
kubectl get nodes $node_name
kubectl get nodes $node_name -o yaml
kubectl describe node $node_name
```

## References

- [Kubernetes : Understanding Kubernetes Objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)