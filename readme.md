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
kubectl argo rollouts get rollout rollouts-demo --watch
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow
kubectl argo rollouts promote rollouts-demo
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:red
kubectl argo rollouts abort rollouts-demo
kubectl argo rollouts set image rollouts-demo rollouts-demo=argoproj/rollouts-demo:yellow
```

BlakYaks demo:

> https://github.com/picklednewtons/argorollout

```bash
kubectl apply -f rollout.yaml
kubectl argo rollouts set image rollout-bluegreen rollouts-demo=argoproj/rollouts-demo:yellow --namespace bg
kubectl argo rollouts promote rollout-bluegreen --namespace bg
kubectl argo rollouts set image rollout-bluegreen rollouts-demo=argoproj/rollouts-demo:red --namespace bg
```

## Clean up

```bash
kubectl delete -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/service.yaml
kubectl delete  -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/rollout.yaml
kubectl delete -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
kubectl delete namespace argo-rollouts
```