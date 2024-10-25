# GitOps @ devfestbari24

## First Steps:
- Install Docker Desktop and enable Kubernetes (https://www.docker.com/products/docker-desktop)
- Install Lens (https://k8slens.dev/download)
- (Optional) Create a github account if you don't have it (https://github.com)
- generate a github access token (https://github.com/settings/tokens - SAVE *GITHUB_ACCESS_TOKEN* IN A DOC, you will need it!!)
- (Optional) Create a Docker Hub account if you don't have it (https://hub.docker.com)
- generate a Docker Hub access token (https://app.docker.com/settings/personal-access-tokens - SAVE *DOCKERHUB_ACCESS_TOKEN* IN A DOC, you will need it!!)

## Second Steps:
Then Open the terminal and launch those command:
- kubectl create namespace ci-cd
- kubectl create namespace dev

Open the terminal and launch this
- kubectl create secret docker-registry docker-cred --docker-server=https://index.docker.io/v1/ --docker-username={*YOUR_USERNAME*} --docker-password={*DOCKERHUB_ACCESS_TOKEN*} -n dev

Start Open Lens and connect to the cluster.
Go on Secrets and create manually:
- docker-hub secret with username (*YOUR_USERNAME*) and password (*DOCKERHUB_ACCESS_TOKEN*) using as namespace ci-cd
- github secret with password *GITHUB_ACCESS_TOKEN* using as namespace ci-cd
