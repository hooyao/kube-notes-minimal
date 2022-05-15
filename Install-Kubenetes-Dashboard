# Install Kubernetes Dashboard

## Install

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
```

A new namespace `kubernetes-dashboard` with its resources are created.

But you can't access the UI at this moment.

## Grant admin access

Save the below yaml to `kubernetes-dashboard-access.yaml`
```yaml
# create a service account
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
# create a cluster binding
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
# create a access token
apiVersion: v1
kind: Secret
metadata:
  name: kubernetes-dashboard-access-token #name the secret as you want
  annotations:
    kubernetes.io/service-account.name: admin-user
type: kubernetes.io/service-account-token
```
Then apply
```bash
kubectl apply -f kubernetes-dashboard-access.yaml
```

## Access Kubernetes-Dashboard UX

Let kubernetes proxy the request to the services
```bash
kubectl proxy
```

Visit `http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy` in browser


Then you see this
![](.attachments/kubenetes-dashboard-login-screen.png)

Choose `Token` and find the token
```bash
kubectl -n kubernetes-dashboard get secret kubernetes-dashboard-access-token -o go-template="{{.data.token | base64decode}}"
# the secret name is kubernetes-dashboard-access-token as we declared
```
Get rid of the last `%`

Now the kubernetes dashboard is ready to go.
![](.attachments/kubenetes-dashboard-home.png)
