# Others

考前準備:

1. 底下四個指令務必滾瓜爛熟
  
  ```sh
  $ kubectl run nginx --image=nginx   (deployment)
  $ kubectl run nginx --image=nginx --restart=Never   (pod)
  $ kubectl run busybox --image=busybox --restart=OnFailure   (job)
  $ kubectl run busybox --image=busybox --schedule="* * * * *"  --restart=OnFailure (cronJob)
  ```

2. 我做了5遍練習題, 和 CKAD 的考題有 80% - 90% 相似度 (https://github.com/dgkanatsios/CKAD-exercises)
答題流程

   1. 考試時一看到題目幾乎是反射動作就用上述的指令產出初步 yaml (--dry-run -o yaml > xxx.yaml)
   2. 然後跳到 kubernets.io 的 tasks (考試的題目幾乎都可以在這裡找到範例, 像 pv/pvc 的 yaml 語法根本不可能背出來, 這裡都有範例,  直接 copy/paste) (https://kubernetes.io/docs/tasks/) 把剩下的部分填入 xxx.yaml
   3. 再用 kubectl create -f xxx.yaml 產出題目所要求的結果
   4. kubectl describe 檢查 deployment 或 pod 是否有正確執行, 有錯馬上刪掉 (kubectl delete deploy/pod) 重來比較快, 修改 xxx.yaml 重新部署
   CKAD 答題時間只有兩小時, 有些題目很長, 分數很少, 立即跳過, 我只作答 82 分, 18 分完全放棄, 我答對 75 分, 超過 CKAD 要求 66% 答對標準 (ps. 我考了兩次才過)

---

