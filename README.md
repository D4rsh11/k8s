# k8s

A full-stack application deployed on Kubernetes, split into a backend service, a frontend UI, and the Kubernetes manifests used to run both.

## Structure

```
.
├── backend/   API service
├── ui/        Frontend application
└── k8s/       Kubernetes manifests
```

## Prerequisites

- Docker
- kubectl
- A Kubernetes cluster (minikube, kind, or a managed cluster)

## Build

Build and tag the images:

```bash
docker build -t <registry>/k8s-backend:latest ./backend
docker build -t <registry>/k8s-ui:latest ./ui
```

Push them if you are using a remote cluster:

```bash
docker push <registry>/k8s-backend:latest
docker push <registry>/k8s-ui:latest
```

## Deploy

Apply the manifests:

```bash
kubectl apply -f k8s/
```

Check the status:

```bash
kubectl get pods
kubectl get svc
```

## Access

Forward the UI service to your machine:

```bash
kubectl port-forward svc/[ui-service-name] 3000:[port]
```

Then open http://localhost:3000.

## Teardown

```bash
kubectl delete -f k8s/
```
