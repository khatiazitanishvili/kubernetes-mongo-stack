# Kubernetes Mongo Stack

This project sets up a MongoDB database and a Mongo Express web-based interface using Kubernetes. It includes all necessary configurations for deploying and managing the stack.

## Project Structure
```
kubernetes-mongo-stack/
├── mongo.yaml              # MongoDB Deployment and Service
├── mongo-configmap.yaml    # ConfigMap for MongoDB connection
├── mongo-express.yaml      # Mongo Express Deployment and Service
├── mongo-secret.yaml       # Secret for MongoDB credentials
└── README.md               # Project documentation
```

## Prerequisites
- Kubernetes cluster (e.g., Minikube, Kind, or a cloud provider)
- `kubectl` installed and configured

## Deployment Steps
1. Apply the Kubernetes Secret:
   ```zsh
   kubectl apply -f mongo-secret.yaml
   ```

2. Apply the ConfigMap:
   ```zsh
   kubectl apply -f mongo-configmap.yaml
   ```

3. Deploy MongoDB:
   ```zsh
   kubectl apply -f mongo.yaml
   ```

4. Deploy Mongo Express:
   ```zsh
   kubectl apply -f mongo-express.yaml
   ```

5. Access Mongo Express:
   - If using Minikube, run:
     ```zsh
     minikube service mongo-express-service
     ```
   - Otherwise, use the external IP of the LoadBalancer service.

## Notes
- Default MongoDB credentials are stored in `mongo-secret.yaml` (base64-encoded).
- Mongo Express connects to MongoDB using the service name `mongodb-service`.

## Cleanup
To delete all resources:
```zsh
kubectl delete -f mongo-express.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-configmap.yaml
kubectl delete -f mongo-secret.yaml
```
