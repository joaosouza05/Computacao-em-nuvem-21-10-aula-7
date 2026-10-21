# Computacao-em-nuvem-21-10-aula-7

kubectl get nodes
kubectl create namespace aula7
kubectl get namespace aula7

kubectl -n aula7 create secret generic credencial-demo --from-literal=senha=exemplo-123
kubectl -n aula7 get secret credencial-demo

apiVersion: v1
kind: Pod
metadata:
  name: leitor-secret
  namespace: aula7
spec:
  containers:
  - name: app
    image: busybox:1.36
    command: ['sh', '-c', 'sleep 3600']
    volumeMounts:
    - name: credencial
      mountPath: /segredos
      readOnly: true
  volumes:
  - name: credencial
    secret:
      secretName: credencial-demo

    kubectl apply -f pod-secret.yaml
kubectl -n aula7 wait --for=condition=Ready pod/leitor-secret --timeout=90s
kubectl -n aula7 exec leitor-secret -- ls /segredos
kubectl -n aula7 exec leitor-secret -- cat /segredos/senha

kubectl -n aula7 create serviceaccount leitor
kubectl -n aula7 get serviceaccount leitor
