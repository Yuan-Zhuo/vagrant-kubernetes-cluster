# vagrant-kubernetes-cluster

Kubernetes cluster automation via Vagrant

# Prerequisites

- virtualbox
  ```
  ## disable bios secure boot
  sudo apt-get install linux-headers-`uname -r`
  sudo apt-get install linux-headers-generic
  sudo apt install virtualbox -y
  wget https://download.virtualbox.org/virtualbox/6.1.34/Oracle_VM_VirtualBox_Extension_Pack-6.1.34.vbox-extpack
  sudo VBoxManage extpack install
  ```
- vagrant
  ```
  curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
  sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
  sudo apt-get update && sudo apt-get install vagrant -y
  vagrant plugin install vagrant-disksize
  ```

# Usage

- bootstrap

  ```
  vagrant up
  ```
- ssh into master

```
vagrant ssh kube-master
kubectl get nodes
```

- deployment & service
  ```
  kubectl apply -f /vagrant/nginx-deployment.yml && kubectl apply -f /vagrant/nginx-service.yml
  ```
