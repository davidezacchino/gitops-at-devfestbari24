# GitOps @ devfestbari24

## First Steps:
- Create a github account if you don't have it (https://github.com)
- Create a Docker Hub account if you don't have it (https://hub.docker.com)
- Install Docker Desktop and enable Kubernetes (https://www.docker.com/products/docker-desktop)
- Install Lens (https://k8slens.dev/download)
- generate a github access token (SAVE IT IN A DOC, you will need it!!)
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
