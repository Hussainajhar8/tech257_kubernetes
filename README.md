# Kubernetes

## Containerise Application

- Install [Kubernetes](installation).
- Retrieve information about services in a Kubernetes cluster: `kubectl get svc`.
- Navigate inside target app folder.
- Run `docker init`.
- Build image: `docker build -t my-app-k8 .`
- Run container: `docker run -d -p 3000:3000 my-app-k8`
- Add tags and push to public:  `docker tag my-app-k8 user/my-app` and`docker push user/my-app`


## Deploy a Kubernetes Cluster with Multiple Pods/Services

- Remove any containers currently running on port 80 to avoid clash: `docker ps`.
- Create a deployment: `kubectl create -f nginx-deploy.yml`.
- To view deployments: `kubectl get deploy`.
- To view pods: `kubectl get pods`.
- This creates the following containers:
- Create a service: `kubectl create -f nginx-service.yml`.
- View services: `kubectl get svc`.
- Access the static website hosted in the Docker image container deployed using Kubernetes: `localhost:30001`.

### Test the Auto-Scaling

- Run `kubectl get pods` - these pods facilitate the deployment live.
- If I delete one of the pods e.g. `kubectl delete pod [pod-name]`, it is automatically replaced in milliseconds. The web app that is deployed using K8s is still running and uninterrupted.

### Delete resources

- Delete existing deployment: `kubectl delete deployment nginx-deployment`
- Delete existing service: `kubectl delete service nginx-svc`

## Deploy Nodejs App

- Create a deployment: `kubectl create -f node-deploy.yml`.
- Create a service: `kubectl create -f node-service.yml`.
- Access the static website hosted in the Docker image container deployed using Kubernetes: `localhost:30002`.

### Delete resources

- Delete existing deployment: `kubectl delete deployment sparta-deployment`
- Delete existing service: `kubectl delete service sparta-svc`


## Two-Tier Deployment

- Application:
- Create deployments: `kubectl create -f node-deploy.yml`.
- Create a service: `kubectl create -f node-service.yml`.

- Database:
- Create a deployment: `kubectl create -f mongo-deploy.yml`.
- Create a service: `kubectl create -f mongo-svc.yml`.
  >Note: to apply changes (rather than delete and recreate): `kubectl apply -f [name].yml`


- Connect database to application.

### Troubleshooting

- Run `kubectl` to see list of commands.
- You can edit a pod, deployment, service etc:
- E.g. `kubectl edit deploy mongo-deploy`, then `:q` to exit.
- You can describe a pod, deployment, service etc:
- E.g. `kubectl describe deploy mongo-deploy`.
