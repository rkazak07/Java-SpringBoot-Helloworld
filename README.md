# For the Springboot Hello world project;

The tools we need are:
Docker
Kubernetes
Maven

First we need app.java which contains the hello world text and we use the hello controller to return the hello world text.
I create my "pom.xml" file with maven so that I can install the required packages. I have the required maven versions in my dockerfile. Just build the Dockerfile directly.

# To deploy Kubernetes manually;

First of all we need a private or public registry to send images to kubernetes.

The Values.yaml File contains Deployment and Service. We revise it according to our own system. We give the information of our repo to Containers in Deployment.
I pushed it to Docker Hub.

# We are creating a namespace.

kubectl create ns test-hello

kubectl appyl -f values.yaml --namespace=test-hello


I specify via nginx-ingress to reach the project via DNS. Currently it is published as http but we have certificates if we want
 Let's specify this with tls secret in ingress.yaml and open it as https. Since I do not have a DNS address, I give fake dns to the host.

Apply kubectl -f ingress.yaml --namespace=test-hello
