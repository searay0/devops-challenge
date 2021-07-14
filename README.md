# DevOps Challenge Option 1
In this demo, a single node Kubernetes cluster will be created with NGINX container images. `nginx-deployment.yml` contains the description for a Kubernetes service account, deployment and service. `secrets.yml` contains the `API_KEY` environment variable. In a public repository, the secrets should not checked into the repository. This file is present here for the purpose of this demo. This demo was run locally on a laptop.

A dedicated service account is used for the deployment and the tokens not mounted in the pods. The pods run as UID 1000.

## Prerequisites
- minikube installed
  - https://minikube.sigs.k8s.io/docs/start/
- Docker installed (Docker is used as driver for minikube)
  - https://docs.docker.com/engine/install/


## Setup
1. Ensure Docker daemon is started
2. start minikube
````bash
minikube start --driver=docker
````
3. Deploy cluster

````bash
kubectl apply -R -f .
````

4. As minikube is running in a Docker container, a tunnel must be created from the host to the container to access the node port. This command provide a URL to access the NGINX web service.

````bash
minikube service nginx-service --url
````

## Rolling Deployment
NGINX can be upgraded by changing the container image version specified in `nginx-deployment.yml`. There are 3 replica pods specified in the deployment. During a deployment, 2 pods will remain up at any point in time.
