# 02-emobilty-exercise-02

As the next warming up exercise, I propose:

- Deploy ArgoCD (in the same local minikube environment)
- Deploy Wordpress stack (Frontend + Backend/MySQL as two separate Docker Containers + Ingress)
- Re-deploy everything again (including Zalando Operator/Postgres) in the real Cloud AWS Sandbox environment (Wojciech Kocjan will help you with that as he built a framework for managing Sandbox environments)

Good Luck !

### Setting up ArgoCD on Minikube

- kubectl create namespace argocd
- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- brew install argocd
- kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
- kubectl port-forward svc/argocd-server -n argocd 8080:443
- Get login password via $ argocd admin initial-password -n argocd
- kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "ClusterIP"}}'

### Setting up wordpress deployment

- kubectl apply -f mysql-deployment.yaml
- kubectl apply -f wordpress-deployment.yaml
- kubectl port-forward svc/wordpress 8081:80
- sudo minikube tunnel
- curl --resolve "wordpress.example:80:127.0.0.1" -i http://wordpress.example
- 127.0.0.1 wordpress.example
- kubectl delete --all namespaces
