# kubernetes-test
1. since we need docker images for deployment in k8 we  are choosing Nginx & Postgres:
2. nginx :latest, postgres:latest

ERRORS:
    

 1.  $ aws eks list-clusters

An error occurred (UnrecognizedClientException) when calling the ListClusters operation: The security token included in the request is invalid.


REsolution:
    We have given wrong AWS Access key & Secret Key





Commands:

1.aws eks list-clusters - to list all clusters.
2. eksctl create cluster --name test --region us-east-1 --nodes 1

Step 3: Configure kubectl to Connect to Your EKS Cluster
    Use aws eks update-kubeconfig to configure kubectl to connect to your EKS cluster:

    aws eks update-kubeconfig --region us-east-1 --name test
        root@ip-172-31-41-202:/home/ubuntu# aws eks update-kubeconfig --region us-east-1 --name test
        Added new context arn:aws:eks:us-east-1:767397701631:cluster/test to /root/.kube/config

kubectl get nodes
