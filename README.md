# Computacao-em-nuvem-21-10-aula-7

kubectl get nodes
kubectl create namespace aula7
kubectl get namespace aula7

kubectl -n aula7 create secret generic credencial-demo --from-literal=senha=exemplo-123
kubectl -n aula7 get secret credencial-demo
