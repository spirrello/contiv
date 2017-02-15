#Contiv

Instructions

1.) Each node should have 2 total nics according to the documentation found here:
http://contiv.github.io/documents/gettingStarted/networking/install-k8s.html
Example:
Add NICS
virsh attach-interface --domain vm7-4 --type bridge --source virbr1 --model virtio --config --live

2.) Run the install_control_node playbook.

3.) Run install_sshkeys playbook without -K but with -k.  Make sure the control_node has gone through the process for itself.

4.) Run install_cluster playbook.


5.) Browse to this page and begin the instructions.
https://github.com/contiv/netplugin/tree/master/install/k8s

kubeadm init must be executed like this:
kubeadm init --api-advertise-addresses [netmaster ip] --service-cidr 10.254.0.0/16   <===This subnet is the contiv service cidr.

****Deploy contiv FIRST BEFORE JOINING NODES:
kubectl apply -f contiv.yaml


6.) BGP

This is needed!
netctl global set --fwd-mode routing    <==== Run Contiv in BGP L3 mode
netctl net create -t default --subnet=20.1.1.0/24/24 default-net   <===== default subnet required
kubectl delete deployment/kube-dns -n kube-system   <===== Run this otherwise netplugin will restart continouslyl
netctl group create -t default default-net default-epg

Add BGP neighbor statements
netctl bgp create [fqdn of worker] -router-ip="[data plan interface]]/24" --as="65002" --neighbor-as="65000" --neighbor="10.10.102.1"

Playbooks

install_control_node.yml:
This playbook prepares the control for deploying Contiv.  It installs the necessary packages for the control node.

install_sshkeys.yml:
This play book generates ssh keys for "user_account" on the "control_node" and distributes them across the workers.


Requirements:
Clean Centos 7 Install with yum update completed.


