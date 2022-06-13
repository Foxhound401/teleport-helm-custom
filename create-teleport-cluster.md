## Prerequisites
- A registered domain name.
- A kubernetes cluster
- Kubernetes >= v1.17.0
- Helm >= 3.4.2


## Install Teleport
Let's start with a single-pod Teleport deployment using a persistent volume as a backend.

```
CLUSTER_NAME="teleport.domain.io"
EMAIL="mail@domain.io"

helm repo add teleport https://charts.releases.teleport.dev

helm install teleport teleport/teleport-cluster --create-namespace --namespace teleport \
  --set clusterName=${CLUSTER_NAME?} --set acme=true --set acmeEmail=${EMAIL?}

```


Teleport's Helm chart uses an external load balancer to create a public IP for Teleport

```
kubectl config set-context --current --namespace=teleport

kubectl get svc

MYIP=$(kubectl get svc teleport -o jsonpath='{.status.loadBalancer.ingress[0].ip}')

echo $MYIP
```

if $MYIP is blank, your cloud provider may have assigned a hostname to the load balancer rather than an IP address. Runt he following command to retrieve the hostname, which you will use in place of $MYIP for subsequent commands.
`MYIP=$(kubectl get svc teleport -o jsonpath'{.status.loadBalancer.ingress[0].hostname}')`

Set up two A DNS records:
- `teleport.domain.io`
- `*.teleport.domain.io`

### Create a Local User

Create user alice who has access to All group.

Save this role as `admin.yaml`

```yaml
kind: role
version: v5
metadata:
  name: admin
spec:
  allow:

```
