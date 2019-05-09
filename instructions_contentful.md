```
# switch to preview cluster
kubectl config use-context mgmt-k8s-001-euw1.quirely.com

# apply the deployment
cd /Users/napcae/code/kubernetes-external-secrets
kubectl apply -f external-secrets.yml
external-secrets.yml has an annotation added: arn:aws:iam::718539334177:role/secret-sync
this role will allow a read only

# create the secret
aws secretsmanager create-secret --region us-west-2 --name hello-service/credentials-new --secret-string '{"username":"admin","password":"12345678"}'

# create an external secret, this tells the CRD to sync from aws secretsmanager to kubernetes secrets
kubectl apply -f hello-service-external-secret.yml


# monitor for errors:
kubectl get pods -n kubernetes-external-secrets

kubectl -n kubernetes-external-secrets logs -f kubernetes-external-secrets-5bb9598864-g8gh4


have a role which the node/pod can assume!
this works wonderfully, you can access to secret now through kubernetes:
kubectl describe secret hello-service -o yaml
```