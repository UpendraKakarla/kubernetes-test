# kubernetes-test
1. since we need docker images for deployment in k8 we  are choosing Nginx & Postgres:
2. nginx :latest, postgres:latest
3. deployment, service, configmap, secrets are done
4. Helmchart


Helmchart :
    prerequisites:  
        

ERRORS:
    

 1.  $ aws eks list-clusters

An error occurred (UnrecognizedClientException) when calling the ListClusters operation: The security token included in the request is invalid.


REsolution:
    We have given wrong AWS Access key & Secret Key

2.root@ip-172-31-41-202:/home/ubuntu/kubernetes-test# kubectl apply -f service.yml
Error from server (BadRequest): error when creating "service.yml": Service in version "v1" cannot be handled as a Service: json: cannot unmarshal object into Go struct field ServiceSpec.spec.selector of type string
Resolution:


root@ip-172-31-41-202:/home/ubuntu/kubernetes-test# kubectl  logs postgres-deployment-644ffd8cff-7mvdf
Error: Database is uninitialized and superuser password is not specified.
       You must specify POSTGRES_PASSWORD to a non-empty value for the
       superuser. For example, "-e POSTGRES_PASSWORD=password" on "docker run".

       You may also use "POSTGRES_HOST_AUTH_METHOD=trust" to allow all
       connections without a password. This is *not* recommended.

       See PostgreSQL documentation about "trust":
       https://www.postgresql.org/docs/current/auth-trust.html



       root@ip-172-31-41-202:/home/ubuntu/kubernetes-test# kubectl apply -f secret.yml
Error from server (BadRequest): error when creating "secret.yml": Secret in version "v1" cannot be handled as a Secret: illegal base64 data at input byte 4

psql: error: connection to server at "a590e1a4af145447c91de7ed0fb8d421-1193114687.us-east-1.elb.amazonaws.com" (54.198.106.196), port 5432 failed: FATAL:  password authentication failed for user "upendra123"


Commands:

1.aws eks list-clusters - to list all clusters.
2. eksctl create cluster --name test --region us-east-1 --nodes 1

Step 3: Configure kubectl to Connect to Your EKS Cluster
    Use aws eks update-kubeconfig to configure kubectl to connect to your EKS cluster:

    aws eks update-kubeconfig --region us-east-1 --name test
        root@ip-172-31-41-202:/home/ubuntu# aws eks update-kubeconfig --region us-east-1 --name test
        Added new context arn:aws:eks:us-east-1:767397701631:cluster/test to /root/.kube/config

kubectl get nodes
psql postgres://postgres:pass123:5432/yourdatabase
psql -h   a590e1a4af145447c91de7ed0fb8d421-1193114687.us-east-1.elb.amazonaws.com   -U postgres -d postgres




