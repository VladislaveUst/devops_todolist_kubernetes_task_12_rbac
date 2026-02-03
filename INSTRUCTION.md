# RBAC Verification Instructions

This guide explains how to verify that the `todoapp` pod has the necessary permissions to list secrets within its namespace.

## Prerequisites
1. Apply the RBAC configuration:
   ```bash
   kubectl apply -f security/rbac.yaml

2. Update the deployment to use the new ServiceAccount:

kubectl apply -f development.yml

3. Execute the following command to verify that the Pod can communicate with the Kubernetes API and list secrets:


kubectl exec -it $(kubectl get pod -l app=todoapp -n todoapp -o jsonpath='{.items[0].metadata.name}') -n todoapp -- sh -c 'curl -s --cacert /var/run/secrets/kubernetes.io/serviceaccount/ca.crt -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" [https://kubernetes.default.svc/api/v1/namespaces/$(cat](https://kubernetes.default.svc/api/v1/namespaces/$(cat) /var/run/secrets/kubernetes.io/serviceaccount/namespace)/secrets'

