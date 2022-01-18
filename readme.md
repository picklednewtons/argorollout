# README

Notes from ArgoRollout build.

## Install

### Argo CLI

> https://argoproj.github.io/argo-rollouts/installation/

Linux install:

```bash
curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64
chmod +x ./kubectl-argo-rollouts-linux-amd64
sudo mv ./kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts
```

Install argo rollout:

```bash
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```

Install examples:

>  https://argoproj.github.io/argo-rollouts/getting-started/

```bash
kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/rollout.yaml
kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/service.yaml
```

Demo rollout commands:

```bash
kubectl argo rollouts list rollouts
kubectl argo rollouts get rollout rollouts-demo --watch
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow
kubectl argo rollouts promote rollouts-demo
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:red
kubectl argo rollouts abort rollouts-demo
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow
```

BlakYaks demo:

> https://github.com/picklednewtons/argorollout


BlueGreen

```bash
kubectl argo rollouts list rollouts -A
kubectl argo rollouts dashboard

kubectl apply -f bluegreen/rollout.yaml
kubectl argo rollouts get rollout rollout-bluegreen --namespace bluegreen --watch

kubectl argo rollouts set image rollout-bluegreen rollouts-demo=argoproj/rollouts-demo:green --namespace bluegreen
kubectl argo rollouts promote rollout-bluegreen --namespace bluegreen

kubectl argo rollouts abort rollout-bluegreen --namespace bluegreen

kubectl argo rollouts set image rollout-bluegreen rollouts-demo=argoproj/rollouts-demo:red --namespace bluegreen

kubectl delete -f bluegreen/rollout.yaml
```

Canary

```bash
kubectl argo rollouts list rollouts -A
kubectl argo rollouts dashboard

kubectl apply -f canary/rollout.yaml
kubectl argo rollouts get rollout rollout-api --namespace canary --watch

kubectl argo rollouts set image rollout-api api=argoproj/rollouts-demo:blue --namespace canary
kubectl argo rollouts promote rollout-api --namespace canary

kubectl argo rollouts set image rollout-api api=argoproj/rollouts-demo:red --namespace canary
kubectl argo rollouts abort rollout-api --namespace canary
kubectl argo rollouts set image rollout-api api=argoproj/rollouts-demo:yellow --namespace canary

kubectl delete -f canary/rollout.yaml
```

## Clean up

```bash
kubectl delete -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/service.yaml
kubectl delete  -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/rollout.yaml
kubectl delete -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
kubectl delete namespace argo-rollouts
```