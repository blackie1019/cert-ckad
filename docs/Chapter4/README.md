# Chapter 4

## Multi-container Pods

將多個 container 放置在同一個 Pod 內

### 3 purpose

- Shared Network

  ![01.png](images/01.png)

- Shared Storage Volumes
  
  ![02.png](images/02.png)

- Shared Process

  ![03.png](images/03.png)

### Multi-container Pods Design Pattern

#### Sidecar Pod

著重於有一個主要(main)的 Pod 與 次要(sidecar) 的 Pod 組合成一個完整功能

![sidecar](images/sidecar.png)

#### Ambassador Pod

著重於集中轉化/再處理 input

![ambassador](images/ambassador.png)

#### Adapter Pod

著重於轉化/再處理 output

![adapter](images/adapter.png)

## Reference

- [Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/#using-a-sidecar-container-with-the-logging-agent)
- [Communicate Between Containers in the Same Pod Using a Shared Volume](https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/)
- [The Distributed System ToolKit: Patterns for Composite Containers](https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/)