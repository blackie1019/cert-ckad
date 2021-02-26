# Pod Design

## Labels, Selectors, and Annotations

```sh
kubectl get pod <pod name> -l <lab=labelname>
kubectl get pod <pod name> -l <lab!=labelname>
kubectl get pod <pod name> -l <lab in (labelname1, labelname2)>
kubectl get pod <pod name> -l <lab1=labelname1,lab2=labelname2>
```

`Label` can be use in Selectors.
`Annotations` can't be use in Selectors.

---

## Deployments

A Deployment defines a desired state for the replica pods.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
  spec:
    containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
          - containerPort: 80
```

- spec.replicas
- spec.selector
- spec.template

```sh
kubectl get deployments
kubectl edot deployment <deployment name>
```

---

## Rolling Updates and Rollbacks

```sh
# Perform a rolling update.
kubectl set image deployment/rolling-deployment nginx=nginx:1.7.9 --record

# Explore the rollout history of the deployment.
kubectl rollout history deployment/rolling-deployment
kubectl rollout history deployment/rolling-deployment --revision=2

# You can roll back to the previous revision like so.
kubectl rollout undo deployment/rolling-deployment

# You can also roll back to a specific earlier revision by providing the revision number.
kubectl rollout undo deployment/rolling-deployment --to-revision=1
```

### Rollback from yaml

spec.strategy.rollingUpdate

- minReadySeconds

  有容器建立後需要一些時間啟動服務，這時候就可以設置這個參數。k8s 會等待設定的時間後再進行升級。如果沒有設定，則 k8s 會在容器一啟動後就直接進行升級服務。

- maxSurge

  1 表示當一個新 Pod 被建立後才會刪除一個舊 Pod，2 表示在更新過程最多會多兩個 Pod 被建立以此類推。此設定也可以為 `%`

- maxUnavailable

  表示在升級過程中，最多可以有幾個 Pod 無法服務。請注意，當 maxSurge 不為 0 的時候，maxUnavailable 也不能為 0。此設定也可以為 `%`

## References

- [Updating a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment)
- [Rolling Back a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment)

---

## Jobs and CronJobs

- Job
  
  `Job` can be used to reliably execute a workload until it completes. Unlike `Pod`, Job usually not running continuously.

  backofLimit => 如果執行時遭遇錯誤，最多可以再重複嘗試執行幾次．

  ```yml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: pi
  spec:
    template:
      spec:
        containers:
        - name: pi
          image: perl
          command: ["perl", "-Mbignum=bpi", "-wle", "print bpi(2000)"]
        restartPolicy: Never
    backoffLimit: 4
  ```

  ```sh
  kubectl get job
  ```

- CronJob

  `CronJob` 

  ```yml
  apiVersion: batch/v1beta1
  kind: CronJob
  metadata:
    name: hello
  spec:
    schedule: "*/1 * * * *"
    jobTemplate:
      spec:
        template:
          spec:
            containers:
              - name: hello
                image: busybox
                args:
                  - /bin/sh
                  - -c
                  - date; echo Hello from the Kubernetes cluster
            restartPolicy: OnFailure
  ```

## References

- [Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)
- [CronJobs]( https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)
- [Automating tasks with CronJobs](https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/)