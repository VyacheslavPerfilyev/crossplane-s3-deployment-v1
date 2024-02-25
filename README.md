# AWS s3 Crossplane Deployment

This project demonstrates deploying an S3 bucket in AWS using Crossplane on a Minikube Kubernetes cluster.

# Prerequisites

* Minikube installed and running.
* Helm installed.
* AWS CLI configured with the necessary credentials.

**Install Crossplane**

Use helm to install crossplane

```shell
helm repo add crossplane-stable https://charts.crossplane.io/stable && helm repo update
helm install crossplane crossplane-stable/crossplane --namespace crossplane-system --create-namespace
```

**Create a Kubernetes secret for AWS**

Add your `aws_access_key_id` and `aws_secret_access_key` to AWS credentials to the `aws-credentials.txt`.

```shell
kubectl create secret generic aws-secret -n crossplane-system --from-file=creds=./aws-credentials.txt
```

**Apply AWS s3 provider config**

```shell
kubectl apply -f manifests/aws-s3-provider-config.yaml
```

**Apply AWS s3 manifests to K8S**

```shell
kubectl apply -f manifests/s3bucket.yaml  
```

**Verify Resource Status**
```shell
kubectl get bucket
```

**Cleanup**
```shell
kubectl delete -f s3bucket.yaml
```
