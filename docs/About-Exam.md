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