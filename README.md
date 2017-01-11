# contiv


Instructions
- Add additional NICs to entire cluster.  Each node should have 3 total nics according to the documentation found here:
http://contiv.github.io/documents/gettingStarted/networking/install-k8s.html
- Run the install_control_node playbook.
- Run install_sshkeys playbook without -K but with -k.  Make sure the control_node has gone through the process for itself.
- Comment out block that begins on line 54 in contiv/k8s/prepare.yml.
- Begin Contiv installation:
http://contiv.github.io/documents/gettingStarted/networking/install-k8s.html



Playbooks

install_control_node.yml:
This playbook prepares the control for deploying Contiv.  It installs the necessary packages for the control node.

install_sshkeys.yml:
This play book generates ssh keys for "user_account" on the "control_node" and distributes them across the workers.
