## Make storage class as Default

```bash
kubectl apply -f storage-class.yaml
kubectl patch storageclass local-storage -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

## Download nginx webserver helm chart

```bash 
helm repo add bitnami https://charts.bitnami.com/bitnami
helm pull bitnami/nginx --version --untar
```

### Download traefik helm chart

```bash
helm repo add traefik https://helm.traefik.io/traefik
helm pull traefik/traefik --version --untar 
```

