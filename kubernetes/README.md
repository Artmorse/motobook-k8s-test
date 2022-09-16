# Kubernetes

## Configure the connection to the registry

- [Documentation](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-in-the-cluster-that-holds-your-authorization-token)

Actually, we use the Docker Hub registry to store our docker images.

Log in on it.

```bash
docker login
```

Then you can check your configuration in [~/.docker/config.json](~/.docker/config.json).

Kubernetes need to accessed to Docker Hub to download the images. We need to create a secret with our credentials.

```bash
k create secret generic regcred \
    --from-file=.dockerconfigjson="$HOME/.docker/config.json" \
    --type=kubernetes.io/dockerconfigjson
```

## Deploy the application

```bash
ka kubernetes/app-deployment.yaml
ka kubernetes/app-service.yaml
```

For development purpose you can create a *port forwarding* to access the pod.

```bash
kubectl port-forward ${POD_NAME} ${LOCAL_PORT}:80
```
