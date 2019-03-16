kubeadm init --apiserver-advertise-address $(hostname -i)

kubectl apply -n kube-system -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 |tr -d '\n')"

kubeadm join 192.168.0.16:6443 --token 34dins.b9vknmqfwjvjz6ig --discovery-token-ca-cert-hash sha256:45b79431232cae139d5424aef36064467e67812d97ed47792015f2519abe64dd

kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml


kubectl port-forward POD_NAME HOST_PORT:CONTAINER_PORT
kubectl port-forward nginx 8080:80


cat debug.yaml
apiVersion: v1
kind: Pod
metadata:
  name: debug
spec:
  containers:
  - name: debug
    image: alpine
    command:
    - "sleep"
    - "10000"

	
kubectl create -f debug.yaml
kubectl exec -i -t debug -- sh

kubectl get po/www -o yaml

kubectl expose pod nginx --name=nginx --type=LoadBalancer