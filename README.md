# Login to EC2 instance
ssh -i ~/.ssh/id_rsa ec2-user@<public_ip>


# Clone this repo in the EC2 instance
git clone git@github.com:rrivera16/clo835_assign2.git


# Change directory
cd assignment2


# Install Docker
Run ./docker-setup.sh


# Logout and login to EC2 instance again and Change Directory


# Create Kind cluster
Run ./kind-setup.sh


# Create namespaces
kubectl create ns mysql
kubectl create ns web

# Create database pod
kubectl apply -f mysql-pod.yaml -n mysql


# Create service for database pod
kubectl apply -f mysql-svc.yaml -n mysql


# Create application pod
kubectl apply -f web-pod.yaml -n web


# Create service for application pods
kubectl apply -f web-svc.yaml -n web

## Create replicasets for database and application pods
kubectl apply -f mysql-repli.yaml -n mysql
kubectl apply -f web-repli.yaml -n web

# Create deployments for database and application pods
kubectl apply -f mysql-deploym.yaml -n mysql
kubectl apply -f web-deploy.yaml -n web