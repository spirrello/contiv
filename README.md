#Contiv

Instructions

1.) Add additional NICs to entire cluster.  Each node should have 3 total nics according to the documentation found here:
http://contiv.github.io/documents/gettingStarted/networking/install-k8s.html
Example:
Add NICS
virsh attach-interface --domain vm7-1 --type bridge --source virbr1 --model virtio --config --live
virsh attach-interface --domain vm7-1 --type bridge --source virbr2 --model virtio --config --live


2.) Run the install_control_node playbook.

3.) Run install_sshkeys playbook without -K but with -k.  Make sure the control_node has gone through the process for itself.

4.) Comment out block that begins on line 54 in contiv/k8s/prepare.yml.

5.) TEMPORARY
Comment out Fluentd section on:
contrib/ansible/roles/node/tasks/main.yml

6.) Begin Contiv installation:
http://contiv.github.io/documents/gettingStarted/networking/install-k8s.html

Run the following from the control node:

- ./prepare.sh <login_userid>
- ./setup_k8s_cluster.sh <login_userid>
- ./verify_cluster.sh <login_userid> 

asdfasdf


Playbooks

install_control_node.yml:
This playbook prepares the control for deploying Contiv.  It installs the necessary packages for the control node.

install_sshkeys.yml:
This play book generates ssh keys for "user_account" on the "control_node" and distributes them across the workers.
