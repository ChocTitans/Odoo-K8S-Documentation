### **Odoo deployment in K8S**


To apply all the resources, run the following command:

`kustomize build . | kubectl apply -f - `

If you want to delete all the resources:

`kustomize build . | kubectl delete -f - `


configmap.env and secret.env are not being used since there's no composite-action, so they're useless.

### Testing

Well since this is a private repo, PSQL and Odoo passwords are hardcoded 

Email : `user@example.com` (You can change them in ./base/deployment.yaml line 62)

Password : `kubectl get secret secret-erp-odoo -o jsonpath="{.data.odoo-password}" | base64 --decode`  "MPCmarIP5v"

For Odoo DB password : 

`kubectl get secret secret-db-postgresql -o jsonpath="{.data.password}" | base64 --decode`





### **Ingress**

Request your domain in AWS ACM. Once the request is approved and the certificate is issued, copy the Certificate ARN in
 `ingress.yaml`

File : `ingress.yaml` (Line 10)
```
    alb.ingress.kubernetes.io/certificate-arn: <yourcertificate> # Certificate ARN in ACM (for your domain)
```

Next, change the domain to your desired domain:

File : `ingress.yaml` (Line 16)
```
    - host: "meilisearch.domain.com"
```

