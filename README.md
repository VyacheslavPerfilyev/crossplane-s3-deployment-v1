# AWS s3 Crossplane Deployment

This project demonstrates deploying an AWS S3 bucket using Crossplane using Minikube Kubernetes cluster.

# Prerequisites

* Minikube and Docker installed and running.
* Helm CLI installed.
* AWS CLI configured with the necessary S3 credentials.

**Start Minikube**
```shell
minikube start --driver=docker
```

**Install Crossplane**

Use Helm CLI to install crossplane

```shell
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
helm install crossplane --namespace crossplane-system --create-namespace --version 1.15.0 crossplane-stable/crossplane
```

**Create a Kubernetes secret for AWS**

Add your `aws_access_key_id` and `aws_secret_access_key` credentials to the `aws-credentials.txt`.

```shell
kubectl create secret generic aws-secret -n crossplane-system --from-file=creds=./aws-credentials.txt
```

**Create AWS S3 Bucket using Crossplane**

*Apply AWS providers*

```shell
kubectl apply -f crossplane/provider-aws-s3.yaml
```
```shell
kubectl apply -f crossplane/provider-aws-config.yaml
```
*Create AWS S3 bucket*
```shell
kubectl apply -f aws-cloud/s3-bucket.yaml  
```
**Verify Resource Status**
```shell
kubectl get bucket
```

**Cleanup**
```shell
kubectl delete -f aws-cloud/s3-bucket.yaml
```
```shell
minikube delete --all
```