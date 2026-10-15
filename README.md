# kubernetes-deploy

Deploying NGINX on a Kubernetes (k3s) cluster running inside an [E2B](https://e2b.dev) sandbox.

## 1. Install the E2B CLI

```bash
npm i -g @e2b/cli
```

## 2. Authenticate

```bash
e2b auth login
```

Or use environment variables (get your keys from the E2B dashboard; never commit them):

```bash
export E2B_API_KEY=<your-e2b-api-key>
export E2B_API_TOKEN=<your-e2b-access-token>
```

## 3. Create the k3s sandbox

```bash
e2b sbx create k3s
```

This starts a sandbox from the `k3s` template and opens a shell in it.

## 4. Deploy NGINX (inside the sandbox)

```bash
kubectl get nodes
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=NodePort
kubectl get pods,svc
```

## 5. Verify

```bash
curl http://localhost:$(kubectl get svc nginx -o jsonpath='{.spec.ports[0].nodePort}')
```

You should see the "Welcome to nginx!" page.

## Notes

- No credentials are stored in this repo.
