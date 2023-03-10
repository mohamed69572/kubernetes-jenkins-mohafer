# Kubernetes Manifests for Jenkins Deployment

Refer https://devopscube.com/setup-jenkins-on-kubernetes-cluster/ for step by step process to use these manifests.

## Puesta en marcha del Jenkins

```
kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes-jenkins/main/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes-jenkins/main/serviceAccount.yaml
kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes-jenkins/main/deployment.yaml
kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes-jenkins/main/volume.yaml
kubectl apply -f https://raw.githubusercontent.com/egibide-ciberseguridad/kubernetes-jenkins/main/service.yaml
```

## Certificado SSL con Let’s Encrypt

1. Nombre de dominio apuntando a la IP pública del HAProxy.

   https://demo-05.ciber-egibide.eu

2. Instalar el cert-manager:

    ```
    kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
    ```

3. [Crear el issuer de Let's Encrypt y configurar el Ingress para que lo use](service-tls.yaml).

## Depuración

Para ver [qué ocurre con la petición](https://cert-manager.io/docs/troubleshooting/acme/#3-troubleshooting-challenges):

```
kubectl -n devops-tools get challenges
kubectl -n devops-tools describe challenge mysite-cert-rbln6-23257799-3404331767
```

## Referencias

- [Setup Jenkins On Kubernetes](https://www.jenkins.io/doc/book/installing/kubernetes/)
- [Use HAProxy Kubernetes Ingress Controller to terminate SSL / TLS](https://www.haproxy.com/documentation/kubernetes/latest/usage/terminate-ssl/)
- [Enable TLS with Let’s Encrypt and the HAProxy Kubernetes Ingress Controller](https://www.haproxy.com/blog/enable-tls-with-lets-encrypt-and-the-haproxy-kubernetes-ingress-controller/)
- [cert-manager](https://github.com/cert-manager/cert-manager)
- [Securing Ingress Resources](https://cert-manager.io/docs/usage/ingress/)
- [Configuring the HTTP01 Ingress solver](https://cert-manager.io/docs/configuration/acme/http01/#configuring-the-http01-ingress-solver)
- [Troubleshooting](https://cert-manager.io/docs/troubleshooting/)
- [Allowing skipping HTTP01 and DNS01 self-check on a per-solver basis](https://github.com/cert-manager/cert-manager/issues/1292)
- [hairpin-proxy](https://github.com/compumike/hairpin-proxy)
- [Rate Limits](https://letsencrypt.org/docs/rate-limits/)
- [Staging Environment](https://letsencrypt.org/docs/staging-environment/)
