# Kubernetes Manifests — Project Documentation

This repository contains example Kubernetes manifests for nginx resources: Pod, Service, Deployment, ReplicaSet, Ingress, and Namespaces.

## Repository files
- [nginx-pod.yaml](nginx-pod.yaml) — simple Pod example
- [nginx-services.yaml](nginx-services.yaml) — Service (ClusterIP) for nginx
- [nginx-deployment.yaml](nginx-deployment.yaml) — Deployment with 3 replicas
- [nginx-replicaset.yaml](nginx-replicaset.yaml) — ReplicaSet example (3 replicas)
- [nginx-ingress.yaml](nginx-ingress.yaml) — Ingress rule for host routing
- [multi_external_api_host.yaml](multi_external_api_host.yaml) — Ingress with multiple hosts
- [nginx-namespaces.yaml](nginx-namespaces.yaml) — Namespace `nginx`
- [carpooling-namespaces.yaml](carpooling-namespaces.yaml) — Namespace `carpooling`
- [.gitignore](.gitignore)
- [.vscode/settings.json](.vscode/settings.json)

## Quickstart / Prerequisites
- Kubernetes cluster (minikube, kind, cloud)
- kubectl configured to target the cluster
- For Ingress examples, enable an ingress controller (e.g., minikube addon enable ingress)

## Common kubectl commands
- Apply a manifest:
  ```sh
  kubectl apply -f <file.yaml>
  ```
- Apply all manifests in repo root:
  ```sh
  kubectl apply -f .
  ```
- Delete a resource:
  ```sh
  kubectl delete -f <file.yaml>
  ```
- List pods:
  ```sh
  kubectl get pods -A
  ```
- Port-forward a service:
  ```sh
  kubectl port-forward service/nginx-service 8083:8082
  ```
- Describe an ingress:
  ```sh
  kubectl describe ingress/nginx-ingress
  ```

## Notes per manifest
- [nginx-pod.yaml](nginx-pod.yaml)
  - Pod named `nginx-pod1`, labels `team: integrations`, `app: todo`.
- [nginx-services.yaml](nginx-services.yaml)
  - ClusterIP service `nginx-service` exposing port 8082 forwarded to container port 80.
  - Examples commented for NodePort and LoadBalancer variants.
- [nginx-deployment.yaml](nginx-deployment.yaml)
  - Deployment `nginx-deployment` in namespace `nginx`, 3 replicas, containerPort 8082.
  - Use `kubectl rollout history deployment/nginx-deployment` and `kubectl rollout undo ...` for rollouts.
- [nginx-replicaset.yaml](nginx-replicaset.yaml)
  - ReplicaSet `nginx-replicaset` with 3 replicas; template labels must match Service selectors.
- [nginx-ingress.yaml](nginx-ingress.yaml)
  - Ingress rule for host `nginx-demo.com` routing `/` to `nginx-service:8082`.
  - To test locally, map your host (minikube IP) in `/etc/hosts`.
- [multi_external_api_host.yaml](multi_external_api_host.yaml)
  - Single Ingress object routing multiple hostnames (`api1.example.com`, `api2.example.com`, `api3.example.com`) to distinct services.

## Example workflow
1. Create namespaces:
   ```sh
   kubectl apply -f nginx-namespaces.yaml
   kubectl apply -f carpooling-namespaces.yaml
   ```
2. Deploy nginx Deployment & Service:
   ```sh
   kubectl apply -f nginx-deployment.yaml
   kubectl apply -f nginx-services.yaml
   ```
3. Verify:
   ```sh
   kubectl get pods -n nginx
   kubectl get svc -n nginx
   ```
4. (Optional) Create Ingress:
   ```sh
   kubectl apply -f nginx-ingress.yaml
   ```
   Add DNS/hosts entry mapping your ingress IP to `nginx-demo.com`.

## Troubleshooting & tips
- Ensure Service selector labels match pod/deployment template labels.
- If Ingress shows no endpoints, verify the ingress controller is running (`kubectl get pods -n ingress-nginx`).
- Use `kubectl get endpoints` to confirm service endpoints.

## License / Notes
This repository contains example manifests for learning and demos. Adjust images, ports, and namespaces to match your environment.
````

Files (quick links):
- [nginx-pod.yaml](nginx-pod.yaml)
- [nginx-services.yaml](nginx-services.yaml)
- [nginx-deployment.yaml](nginx-deployment.yaml)
- [nginx-replicaset.yaml](nginx-replicaset.yaml)
- [nginx-ingress.yaml](nginx-ingress.yaml)
- [multi_external_api_host.yaml](multi_external_api_host.yaml)
- [nginx-namespaces.yaml](nginx-namespaces.yaml)
- [carpooling-namespaces.yaml](carpooling-namespaces.yaml)
- [.gitignore](.gitignore)
- [.vscode/settings.json](.vscode/settings.json)Files (quick links):
- [nginx-pod.yaml](nginx-pod.yaml)
- [nginx-services.yaml](nginx-services.yaml)
- [nginx-deployment.yaml](nginx-deployment.yaml)
- [nginx-replicaset.yaml](nginx-replicaset.yaml)
- [nginx-ingress.yaml](nginx-ingress.yaml)
- [multi_external_api_host.yaml](multi_external_api_host.yaml)
- [nginx-namespaces.yaml](nginx-namespaces.yaml)
- [carpooling-namespaces.yaml](carpooling-namespaces.yaml)
- [.gitignore](.gitignore)
- [.vscode/settings.json](.vscode/settings.json)