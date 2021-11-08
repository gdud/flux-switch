# flux-switch


## Create test cluster:

```
kind create cluster --name flux-switch
```

## Bootstrap Flux

https://fluxcd.io/docs/installation/#github-and-github-enterprise

```
export GITHUB_TOKEN=<your-token>
```

```
flux bootstrap github \
  --owner=gdud \
  --repository=flux-switch \
  --personal
```

## Change branch main -> v2

```
flux suspend source git flux-system -n flux-system
```

```
kubectl edit gitrepository flux-system -n flux-system
```

... set `spec.ref.branch` to `v2` and then...

```
flux resume source git flux-system -n flux-system & flux reconcile kustomization flux-system --with-source 
```