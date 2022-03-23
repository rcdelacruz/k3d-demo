#################################
# K3d                           #
# How to run Kubernetes locally #
# https://youtu.be/mCesuGk-Fks  #
#################################

# Referenced videos:
# - How to run local multi-node Kubernetes clusters using kind: https://youtu.be/C0v5gJSWuSo
# - Kaniko - Building Container Images In Kubernetes Without Docker: https://youtu.be/EgwVQN6GNJg

#########
# Setup #
#########

# Install `k3d` CLI (https://k3d.io/#installation)

#################################
# Creating single-node clusters #
#################################

export KUBECONFIG=$PWD/kubeconfig.yaml

k3d cluster create my-cluster

docker container ls

kubectl get pods -A

kubectl get nodes

################################
# Creating additional clusters #
################################

k3d cluster create another-cluster \
    --image rancher/k3s:v1.20.4-k3s1

docker container ls

#####################
# Deleting clusters #
#####################

k3d cluster delete my-cluster

k3d cluster delete another-cluster

#####################################
# Creating clusters through configs #
#####################################

git clone https://github.com/vfarcic/k3d-demo.git

cd k3d-demo

cat k3d.yaml

k3d cluster create --config k3d.yaml

kubectl get nodes

kubectl apply --filename k8s/

# Open http://localhost in a browser

#####################
# Deleting clusters #
#####################

k3d cluster delete my-cluster

###########################
# Speed test against kind #
###########################

docker system prune -a -f --volumes

k3d cluster create my-cluster

k3d cluster delete my-cluster

# Please watch https://youtu.be/C0v5gJSWuSo if you are not already familiar with kind
kind create cluster --name my-cluster

kind delete cluster --name my-cluster
