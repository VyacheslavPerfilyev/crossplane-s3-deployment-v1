# Crossplane AWS S3 Deployment

This project demonstrates deploying an S3 bucket in AWS using Crossplane on a Kubernetes cluster.
Crossplane enables managing cloud infrastructure using Kubernetes resources, providing a unified API for provisioning and managing cloud services.

# Prerequisites

* A Kubernetes cluster up and running.
* AWS CLI configured with the necessary credentials.
* Crossplane installed.



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