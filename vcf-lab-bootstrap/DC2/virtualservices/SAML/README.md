OKD AVI Ansible script to deploy loadbalancing vips on AVI

Change the file build_lb_vars.yml to match your needs.
Placement network, ip addresses of the nodes.
Important note: When you are bootstrapping, change to bootstrap server state to true in pool section. i.e:
{
 "ip": { "addr": 100.64.35.99, "type": V4 },
 "hostname": "okd4-bootstrap",
 "enabled": "true",
},


To deploy
ansible-playbook deploy.yml

To remove
ansible-playbook cleanup.yml --extra-vars "state=absent"
