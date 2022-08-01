# microk8s-ansible
Ansible playbooks for installing microk8s.

Node that you should update the hosts.ini file to point at "all" of your hosts.  For experimentation, it was convenient (though not necessary) to use the "sample" group of hosts, rather than the "all" group.

Typically use the AptUpdate... playbook to ensure the installed OS is fully updated, and rebooted if needed.
Use the K8sInstall... playbook to perform the basic installation
Use the K8sJoin... playbook to link up all the nodes to the first node. (i.e., the first node supplies the Join command that is  used by all the other nodes.

The playbooks seemed to work on both the Ubuntu and Rasbian 64 bit OS installations on Raspberry Pi 4 hosts.

Note that for some reason, the Raspbian implementation does not sufficiently set the path for use by ansible, and individual commands submitted via ansible must use the fully qualified path name.    For example, the following will work on Ubuntu after completing the installation and joining of the nodes:
ansible all -a "microk3s kubectl get nodes"
but that command will NOT work on the Rasbian install, and you will need:
ansible all -a "/snap/bin/microk3s kubectl get nodes"

