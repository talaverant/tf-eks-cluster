# Provision an EKS Cluster using TF-Controller from Weaveworks

This repo is a companion repo to the [Provision an EKS Cluster learn guide](https://learn.hashicorp.com/terraform/kubernetes/provision-eks-cluster), containing
- Terraform configuration files to provision an EKS cluster on AWS.
- Terraform custom resource to manage the tf resources defined in the above configuration files.

Here are the steps to make this run properly:
1. I did use a KinD Cluster but feel free to use another type of k8s cluster (changes may apply though)
2. Deploy FluxCD on your cluster in one of the way described [here](https://fluxcd.io/docs/installation/)
3. Create a secret on your cluster for AWS Authentication purposes:
  ```
cat <<EOF | kubectl apply -f -
  ---
apiVersion: v1
kind: Secret
metadata:
&nbsp  &nbspname: aws-credentials
&nbsp  &nbspnamespace: flux-system
data:
&nbsp  &nbspaccess_key: <<64bEncoded-AWS-Access-key-ID>>
&nbsp  &nbspsecret_key: <<64bEncoded-AWS-Secret-access-key>>
EOF
```
