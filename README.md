
#  Deploying Super Mario on Kubernetes

Super Mario is a classic game loved by many. In this guide, we'll explore how to deploy a Super Mario game on Amazon's Elastic Kubernetes Service (EKS). Utilizing Kubernetes, we can orchestrate the game's deployment on AWS EKS, allowing for scalability, reliability, and easy management

## Let's Deploy
#### Step 1. Launch Ubuntu instance

Choose ubuntu server and select t2.micro as your instance type.

Create IAM role and assign ec2 server you have created 

For permission policy select Administrator Access (Just for learning purpose)

#### Step 2. Cluster provision
```
git clone https://github.com/NirmalNaveen20/supermario-k8s.git
```

Change the directory

```
cd supermario-k8s
```

Provide the executable permission to script.sh file, and run it.

`sudo chmod +x script.sh`

`./script.sh`

This script will install Terraform, AWS cli, Kubectl, Docker.

Check versions:

`docker --version`

`aws --version`

`kubectl version --client`

`terraform --version`

Now change directory into the EKS-TF

Run Terraform init

NOTE: Don’t forgot to change the s3 bucket name in the backend.tf file

`cd EKS-TF`

`terraform init`

Now run terraform validate and terraform plan

`terraform validate`

`terraform plan`

Now Run terraform apply to provision cluster.

```terraform apply --auto-approve```

#### Step 2. Kubernetes Configuration

Update the Kubernetes configuration

Make sure change your desired region

```aws eks update-kubeconfig --name EKS_CLOUD --region us-east-1```

Let’s apply the deployment and service

Deployment

`kubectl apply -f deployment.yaml`
#to check the deployment 

`kubectl get all`



Now let’s apply the service

Service

`kubectl apply -f service.yaml`

`kubectl get all`


Now let’s describe the service and copy the LoadBalancer Ingress

```
kubectl describe service mario-service
```

Paste the ingress link in a browser and you will see the Mario game.

Let’s Go back to 1985 and play the game like children.

This is official image by MR CLOUD BOOK

You can check in Docker-hub as well nirmalnaveen/supermario

#### Let's remove the service and deployments

`kubectl get all`

`kubectl delete service mario-service`

`kubectl delete deployment mario-deployment`

`terraform destroy --auto-approve`





⚠Note: 

Don’t forget to Stop or Delete all clusters and services of AWS otherwise this will cost you without knowing you.

## Author

- [@Nirmal Naveen](https://www.nirmalnaveen.com/)

![Logo](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTlPjhPV6D68kBoBq82reUr6ndqcI_n9YPSQ9WA3sqT_RAXpDVcujzTO1MmWrcmcGYeyA&usqp=CAU)


