### ArgoCD

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# port-forward to access through browser
kubectl port-forward svc/argocd-server 8080:80 -n argocd 

# Get the secret yaml
kubectl get secret argocd-secret -n argocd -o yaml

# Get the password
kubectl get secret argocd-secret -n argocd -o jsonpath="{.data.admin\.password}" | base64 -d; echo

# reset the password by patching the secret
kubectl patch secret argocd-secret -n argocd \
  -p '{"stringData": {"admin.password": "'$(htpasswd -bnBC 10 "" passW0Rd | tr -d ':\n')'", "admin.passwordMtime": "'$(date +%FT%T%Z)'"}}'


# install argocd cli

brew install argocd  <!---- # with homebrew -- run as administrator -->



# Logging into argocd server through argocd cli.

- export ARGOCD_SERVER=localhost:8080
- export
- argocd login $ARGOCD_SERVER
-argocd repo add git@github.com:Johnstx/terraform-aws-pipeline.git --ssh-private-key-path /home/stax/.ssh/id_rsa

# Add a cluster to ArgoCD (optional)

# Deploy an Application
- argocd app create -f /mnt/c/Users/USER/Documents/staxxwrkspace/kubernetes/terraform-aws-pipeline/terraform-aws-pipeline/argocd/apps/basic-app.yaml


### kube-state-metrics
-  argocd app create -f C:\Users\USER\Documents\staxxwrkspace\kubernetes\terraform-aws-pipeline\terraform-aws-pipeline\argocd\apps\kube-prometheus-stack.yaml

### Delete an application
-  argocd app delete kube-prometheus-stack

### Grafana
-  kubectl port-forward svc/kube-prometheus-stack-grafana 3000:80 -n monitoring
-  kubectl get secret --namespace monitoring kube-prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
