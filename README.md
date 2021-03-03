# Practices for CKAD

Main Course from [Certified Kubernetes Application Developer (CKAD)](https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/)

---

## Setup Terminal

Kubectl autocomplete and alias `k`

```sh
source <(kubectl completion bash) # setup autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.

alias k=kubectl
complete -F __start_kubectl k
```

Ref to [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## CKAD Exercises

- [CKAD Exercises](https://github.com/dgkanatsios/CKAD-exercises)
- [Kubernetes documentation - Tasks](https://kubernetes.io/docs/tasks/)

### Important

- Easily create the pod that was just described using YAML:
  
  ```sh
  kubectl run nginx --image=nginx --restart=Never --dry-run=client -n mynamespace -o yaml > pod.yaml
  kubectl create -f pod.yaml
  ```sh

- Most quick way to create a object
  
  ```sh
  kubectl run nginx --image=nginx   (deployment)
  kubectl run nginx --image=nginx --restart=Never   (pod)
  kubectl run busybox --image=busybox --restart=OnFailure   (job)
  kubectl run busybox --image=busybox --schedule="* * * * *"  --restart=OnFailure (cronJob)
  ```

## Resources allowed during exam

During the exam, candidates may:

- review the Exam content instructions that are presented in the command line terminal
- review Documents installed by the distribution (i.e. /usr/share and its subdirectories)
- use their Chrome or Chromium browser to open one additional tab in order to access assets at: https://kubernetes.io/docs/, https://github.com/kubernetes/,  https://kubernetes.io/blog/ and their subdomains. This includes all available language translations of these pages (e.g. https://kubernetes.io/zh/docs/)
- No other tabs may be opened and no other sites may be navigated to   (including https://discuss.kubernetes.io/). 

*The allowed sites above may contain links that point to external sites. It is the responsibility of the candidate not to click on any links that cause them to navigate to a domain that is not allowed.*

---

## Sections

### Chapter 2

- `Pod` or `Deployment`

- [About *Cloud Native - Certified Kubernetes Application Developer (CKAD)* exam](docs/About-Exam.md)
- [Chapter 2.1 : Build Your Practice Cluster](docs/Chapter2.1_Build-Your-Practice-Cluster/README.md)
- [Chapter 2.2 : Kubernetes API Primitives](docs/Chapter2.2_Kubernetes-API-Primitives/README.md)
- [Chapter 2.3 : Creating Pods](docs/Chapter2.3_Creating-Pods/README.md)
- [Chapter 2.4 : Namespaces](docs/Chapter2.4_Namespaces/README.md)
- [Chapter 2.5 : Basic Container Configuration](docs/Chapter2.5_Basic-Container-Configuration/README.md)

### Chapter 3

- `ConfigMap`
- `SecurityContexts`
- `Resource Requirements`
- `Secrets`
- `ServiceAccounts`

[Chapter 3](docs/Chapter3/README.md)

### Chapter 4

- Shared Network

  ![01.png](/docs/Chapter4/images/01.png)

- Shared Storage Volumes
  
  ![02.png](/docs/Chapter4/images/02.png)

- Shared Process

  ![03.png](/docs/Chapter4/images/03.png)

[Chapter 4](docs/Chapter4/README.md)

### Chapter 5

- Probes
- Logs command
- Installing Metrics Server
- Top command
- Debugging

[Chapter 5](docs/Chapter5/README.md)

### Chapter 6

- Labels, Selectors, and Annotations
- Deployments
- Rolling Updates and Rollbacks
- Jobs and CronJobs

[Chapter 6](docs/Chapter6/README.md)

### Chapter 7

[Chapter 7](doc/../docs/Chapter7/README.md)

### Chapter 8

TBD

### Chapter 9

TBD

### Chapter 10

TBD

---

## Others

[others](docs/others/README.md)

---

## References

- [Kubernetes Documentation - Available Documentation Versions](https://kubernetes.io/docs/home/supported-doc-versions/)
- [Important Instructions: CKA and CKAD](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
- [CKAD Exam Overview](https://medium.com/@devops.rutik/ckad-exam-overview-4172edfb086)