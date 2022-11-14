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

download & install cert-manager
```bash
helm repo add jetstack https://charts.jetstack.io
helm pull jetstack/cert-manager --version v1.10.0 --untar
helm install cert-manager cert-manager -set installCRDs=true
```

An issuer is a CRD of cert-manager API, that was why we needed to install cert-manager

install issuer manually,
```bash
kubectl apply -f issuer.yaml
```

#### Checking certificates

```bash
kubectl get secret 

NAME                                 TYPE                 DATA   AGE
dev.goacademy.io-tls-xp7r7           Opaque               1      4m40s
```
you can find that the secret has some suffix name, this for the certificate rotation, we need to wait till the  issuer creates a valid certificate,
it will take few minutes. Then a valid certificate with name `dev.goacademy.io-tls` will be created.

*Check the issuer*
If the secret is not created, then check the issuer, 

```bash
k get issuer
NAME          READY   AGE
letsencrypt   True    63s

k describe issuer letsencrypt
```
Check if there are any error in the issuer, if there are no errors then wait till the certificate is created. 

```bash
kubectl get secret go-academy.io-tls -o json | jq -r '.data."tls.crt"' | base64 -d | openssl x509 -dates -noout -issuer
```
### Installing harbor 

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm pull bitnami/harbor --version 16.0.0 --untar 
```




