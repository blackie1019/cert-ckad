# Chapter 5 - Observability

## Liveness and Readiness Probes

https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/learn/e91d7010-d4e8-4d3c-8894-212900fd09bd/a116f79a-0f93-4fbe-b79f-c985c29541ff/watch

- Probes

  由於 k8s 會自動重啟你的 `pods`(預設)，所以有時候我們可以自定義決定 k8s 如何核定容器內的狀態(status). 可以用來決定何時準備好可運行第一個 `command` 或是準備接受第一個 `request`.

- Liveness Probe

  Indicates whether the container is running properly, and governs when the cluster will automatically stop or restart the container.

- Readiness Probe

  Indicates whether the container is ready to service requests and governs whether requests will be forwarded to the pod.

- Startup Probe

  TBD

### 參數

- initialDelaySeconds: 當啟動Liveness probe 或是 Readiness Probe 的條件準備好後, 要延遲多久才執行
- periodSeconds: 多久重新執行一次

*使用 startup probes 來保護啟動較慢的容器*

## References

- [Container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes)
- [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

---

## Container Logging

---

## Installing Metrics Server

---

## Monitoring Applications

---

## Debugging

---

## Lab
