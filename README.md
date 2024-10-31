# GitOps @ devfestbari24

## First Steps:
- Install Docker Desktop and enable Kubernetes (https://www.docker.com/products/docker-desktop)
- Install Lens (https://k8slens.dev/download)
- (Optional) Create a github account if you don't have it (https://github.com)
- generate a github access token (SAVE IT IN A DOC, you will need it!!)
- (Optional) Create a Docker Hub account if you don't have it (https://hub.docker.com)
- generate a Docker Hub access token (SAVE IT IN A DOC, you will need it!!)

## Second Steps:
Then Open the terminal and launch those command:
- kubectl create namespace ci-cd
- kubectl create namespace dev

Open the terminal and launch this
- kubectl create secret docker-registry docker-cred --docker-server=https://index.docker.io/v1/ --docker-username={YOUR_USERNAME} --docker-password={YOUR_PASSWORD} -n dev

Start Open Lens and connect to the cluster.
Go on Secrets and create manually:
- docker-hub secret with username (docker username) and password (docker access token you got before) using as namespace ci-cd
- github secret with password (github access token you got before) using as namespace ci-cd

# Installing ARGOCD
- kubectl apply -n ci-cd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- kubectl -n ci-cd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
- kubectl port-forward svc/argocd-server -n ci-cd 8080:443

# TEKTON PIPELINE
- kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
- kubectl apply --filename  https://storage.googleapis.com/tekton-releases/dashboard/latest/release-full.yaml
- kubectl apply -f kubernetes-config/tekton/tekton.yaml
- kubectl port-forward -n tekton-pipelines service/tekton-dashboard 9097:9097
- http://localhost:9097

# KUBESEAL to encrypt secrets
- helm repo add sealed-secrets https://bitnami-labs.github.io/sealed-secrets
- helm dependency update sealed-secrets
- helm install sealed-secrets sealed-secrets/sealed-secrets --namespace ci-cd --version 2.7.4

# To seal secret
- kubeseal --format=yaml --controller-name=sealed-secrets --controller-namespace=ci-cd -f argocd-springboot-service-infra-repository.yaml > argocd-springboot-service-infra-repository-enc.yaml

# Deploying Steps
- you must create three github project:
  - argocd-cluster-config
  - argocd-springboot-service
  - argocd-springboot-service-infra

Now we need to connect only argocd-cluster-config on ArgoCD:
- go on localhost:8080
- go on Settings/Repository and click to "Connect Repo"
- now you need to copy the https link from your git repo and compile the form
- After that return to Applications and Click on Create New App
- Compile the form

