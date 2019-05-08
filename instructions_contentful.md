kubectl config use-context mgmt-k8s-001-euw1.quirely.com
cd /Users/napcae/code/kubernetes-external-secrets
kubectl apply -f external-secrets.yml
aws secretsmanager create-secret --region eu-west-1 --name hello-service/credentials-new --secret-string '{"username":"admin","password":"12345678"}'

kubectl apply -f hello-service-external-secret.yml

monitor:
kubectl get pods -n kubernetes-external-secrets

kubectl -n kubernetes-external-secrets logs -f kubernetes-external-secrets-5bb9598864-g8gh4


have a role which the node/pod can assume!

this works wonderfully