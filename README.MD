ansible-playbook deploy_controller.yml
ansible-playbook upgrade.yml
ansible-playbook configure_no_access_cloud.yml
ansible-playbook deploy_ses.yml


For installing openshift user

- create ssh key. This needed for ssh to the openshift nodes.
- create a segment with dhcp for the openshift nodes.
- Config AVI. use the ingress vip and api vip in the installer.
- openshift-installer create install-config
  follow the steps. this will create an install config. Edit the config and change master and worker nodes where needed. i.e. 1 and 1
- openshift-installer create cluster --dir .
  This creates the openshift cluster
- When the bootstrap and master are booting, add them to the AVI pool.
- When the worker node is booting, check the ip and add to AVI pool.


