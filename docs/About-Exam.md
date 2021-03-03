# Cloud Native - Certified Kubernetes Application Developer (CKAD)

[Cloud Native - Certified Kubernetes Application Developer (CKAD)](https://www.cncf.io/certification/ckad/)

The successful candidate will be comfortable using:

- An OCI-Compliant Container Runtime, such as Docker or rkt.
- Cloud native application concepts and architectures.
- A programming language, such as Python, Node.js, Go, or Java.

Exam details
The online, proctored, performance-based test consists of a set of performance-based items (problems) to be solved in a command line and is expected to take approximately two (2) hours to complete.

This exam curriculum includes these general domains and their weights on the exam:

- 13% – Core Concepts
- 18% – Configuration
- 10% – Multi-Container Pods
- 18% – Observability
- 20% – Pod Design
- 13% – Services & Networking
- 8% – State Persistence

Quarterly exam updates are planned to match Kubernetes releases. Please see [the FAQ](http://training.linuxfoundation.org/go/cka-ckad-faq) for the current exam environment version.

## What are the system requirements to take the exam?  

Exams are delivered online and Candidates must provide their own computer with:

- Current version of Chrome or Chromium

  - you don’t need to install a virtual machine, use a client machine, or anything beyond a Chrome or Chromium browser
  - Make sure you have third party cookies turned on for the duration of the exam.

- Reliable internet access

  - Turn off bandwidth-intensive services (e.g. file sync, dropbox, BitTorrent)
  - Ask others who may be sharing your Internet connection not to stream video or download large files.

- Microphone

  - Please check to make sure it is working before you start your exam session.

- Webcam
  
  - Ensure the webcam is capable of being moved as the proctor may ask you to pan your surroundings to check for potential violations of exam policy.
  - Try holding up your ID while viewing your webcam feed to ensure your placement and resolution are sufficient for the person viewing your feed to read your ID.
  - If you will be testing from an employer-provide ISP or will use an employer provided machine, please ensure that streaming will be allowed using WebRTC.
 
Candidates should run the [compatibility check tool](https://www.examslocal.com/ScheduleExam/Home/CompatibilityCheck) to verify that their hardware meets the minimum requirements.

## What resources am I allowed to access during my exam?

During the CKA & CKAD exam, candidates may:

- review the Exam content instructions that are presented in the command line terminal
- review Documents installed by the distribution (i.e. /usr/share and its subdirectories)
- use their Chrome or Chromium browser to open one additional tab in order to access assets at: https://kubernetes.io/docs/, https://github.com/kubernetes/,  https://kubernetes.io/blog/ and their subdomains. This includes all available language translations of these pages (e.g. https://kubernetes.io/zh/docs/)

No other tabs may be opened and no other sites may be navigated to   (including https://discuss.kubernetes.io/). 

The allowed sites above may contain links that point to external sites. It is the responsibility of the candidate not to click on any links that cause them to navigate to a domain that is not allowed.

## What application version is running in the Exam Environment?

- The CKA exam environment is currently running Kubernetes v1.20
- The CKAD exam environment is currently running Kubernetes v1.20

The CKA and CKAD exam environment will be aligned with the most recent K8s minor version within approximately 4 to 8 weeks of the K8s release date.


## CKAD Environment

https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad#cka-and-ckad-environment

|Cluster| Members| CNI| Description|
|:----|:----|:----|:----|
|k8s| 1 master 2 worker| flannel| k8s cluster|
|dk8s|  1 master 1 worker| flannel| k8s cluster|
|nk8s|  1 master 2 worker|  calico|  k8s cluster|
|sk8s| 1 master 1 worker| flannel| k8s cluster|

---

## 

[https://github.com/yuyicai/cka-ckad-exam-experience](https://github.com/yuyicai/cka-ckad-exam-experience)

- 考试难度

  总的来说CKA考试还是相对简单的，如果你有k8s生产环境维护使用经验，大可以直接考试，过线是没问题的 ；CKAD难度也不大，题量较CKA大，需要注意每道题不超过6分钟

- kubectl自动补全

  注意使用kubectl自动补全，考试环境默认已经配置了kubectl自动补全，无需考生另行配置，但是这还不够，我们可以用k代替kubectl kubectl Cheat Sheet

  ```sh
  alias k=kubectl
  complete -F __start_kubectl k
  ```

- 使用考试环境提供的记事本

  使用记事本，考试过程中，最好将使用过的命令记录到记事本，后面的题目可以稍微改动再使用（特别是创建pod的命令，估计要使用七八次吧）

- 使用--dry-run生成yaml

  使用`--dry-run`参数来生成一个基础的yaml，再按照题目要求修改这个基础yaml文件，不要纯手写yaml。如果题目无特殊要求，能kubectl命令完成的就不要使用yaml文件，这个比较浪费时间。

- 浏览器收藏夹

  将上面备考中的github仓库练习题中提到的官方文档保存到浏览器收藏夹，这样做的目的是在浏览器地址栏输入关键词，就会弹出收藏好的官方文档地址，就可以直达对应的文档，不需要在官方文档上再一次搜索

- vim编辑器

  vim编辑器要求不高，但是你至少要知道如何进入编辑模式，如何保存文档，复制粘贴之类的快捷键记不记都行，可以右键复制粘贴

- web终端中的复制粘贴

  web终端中无法使用`Ctrl+C`、`Ctrl+V`（考试提供的记事本可以使用），使用`Ctrl + Insert`，`Shift + Insert`代替，web终端中也可以使用右键复制粘贴