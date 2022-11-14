## Make storage class as Default

```bash
kubectl apply -f storage-class.yaml
kubectl patch storageclass local-storage -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

### Nginx

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm pull bitnami/nginx --version --untar
```

### Traefik

```bash
helm repo add traefik https://helm.traefik.io/traefik
helm pull traefik/traefik --version --untar 
```

### Cert-manager

cluster issuer can be installed manually or can be installed directly using the flag `-set installCRDs=true`

```bash
helm repo add jetstack https://charts.jetstack.io
helm pull jetstack/cert-manager --version v1.10.0 --untar
helm install cert-manager cert-manager -set installCRDs=true
```



