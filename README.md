# contiv


Instructions
- Run the install_control_node playbook 1st.
- Run install_sshkeys playbook generates an ssh key on the control node and then distributes it to the other nodes.



Playbooks
install_control_node.yml:
This playbook prepares the control for deploying Contiv.  It installs the necessary packages for the control node.

install_sshkeys.yml:
This play book generates ssh keys for the user and distributes them across the nodes.
