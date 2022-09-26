## k8s-simple-app
Simple example apps using ingress with different types:
- Same host with different paths
- Different hosts
- Different hosts using https

## Install K8s cluster with Kops
- Instal Kops cli `brew update && brew install kops`
- Create a S3 Bucket in you AWS Account, for this example I'll use the bucket clederson.com
- Create an environment variable to use with Kops cli `export KOPS_STATE_STORE=s3://clederson.com`
- Create the cluster config with Kops `kops create cluster --zones=us-east-2a k8sdev.clederson.com --state=s3://clederson.com --node-count=2`
- Update the cluster config and create it `kops update cluster k8sdev.clederson.com --yes --admin`
- Run the Kops validator and wait until the cluster is created `kops edit cluster k8sdev.clederson.com`
- Install Nginx with Helm
```
kubectl create ns nginx-ingress
kubens nginx-ingress
helm install stable/nginx-ingress --generate-name
````
- Update in your DNS Zone the loadbalancer name created by NgInx service
- Once is finished, delete the cluster `kops delete cluster k8sdev.clederson.com --yes`



