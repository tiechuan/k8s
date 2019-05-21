
# windows 10 pro
# Hyper-V
# https://docs.docker.com/machine/drivers/hyper-v/


# Installation of Chocolatey is easy, just use the following command from PowerShell in administrative mode
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString(‘https://chocolatey.org/install.ps1'))

###################################################################################################

# you are using Chocolatey (recommended), then you can install docker-for-windows with the following command
choco install docker-for-windows -pre

# enable Hyper-V using the following command in PowerShell with administrative support. Note that enabling/disabling hyper-v hypervisor requires a restart of your local machine.
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All


kubectl get nodes
kubectl config view

kubectl config get-contexts
kubectl config use-context minikube


###################################################################################################
choco install minikube -y

# Identify physical network adapters ( Ethernet and/or Wifi) using the command
Get-NetAdapter

# create a new hyper-v switch
New-VMSwitch -Name “miniCluster” -AllowManagement $True -NetAdapterName “Ethernet”

# create cluster
# you can view the VM in Hyper-V manager
minikube start — vm-driver=hyperv — hyperv-virtual-switch="miniCluster"

minikube dashboard

kubectl run nginx --image=nginx

minikube docker-env
minikube ip
# connect to minikube from docker client
& minikube docker-env | Invoke-Expression


kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.10 --port=8080
kubectl expose deployment hello-minikube --type=NodePort
kubectl get pod
minikube service hello-minikube --url
kubectl delete services hello-minikube
kubectl delete deployment hello-minikube
