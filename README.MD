ansible-playbook deploy_controller.yml
ansible-playbook upgrade.yml
ansible-playbook configure_no_access_cloud.yml
ansible-playbook deploy_ses.yml

#Configure Vault Alert script.
ansible-playbook configure_vault.yml

For installing openshift user

- create ssh key. This needed for ssh to the openshift nodes.
- create a segment with dhcp for the openshift nodes.
- Config AVI. use the ingress vip and api vip in the installer.
- you need to add  the certs to trusted.
  *ubuntu*
  sudo apt-get install ca-certificates curl gnupg
  follow the redhat steps
  wget https://wdc-06-vc12.oc.vmware.com/certs/download.zip --no-check-certificate
  cp certs/lin/* /etc/ssl/certs/
  update-ca-certificates

  *redhat*
  https://docs.openshift.com/container-platform/4.13/installing/installing_vsphere/installing-vsphere-installer-provisioned.html#installation-adding-vcenter-root-certificates_installing-vsphere-installer-provisioned

- openshift-installer create install-config
  follow the steps. this will create an install config. Edit the config and change master and worker nodes where needed. i.e. 1 and 1
- openshift-installer create cluster --dir .
  This creates the openshift cluster
- When the bootstrap and master are booting, add them to the AVI pool.
- When the worker node is booting, check the ip and add to AVI pool.


Here is an example for install-config.yaml

additionalTrustBundlePolicy: Proxyonly
apiVersion: v1
baseDomain: okd.nordic.fqdn.nl
compute:
- architecture: amd64
  hyperthreading: Enabled
  name: worker
  platform: {}
  replicas: 1
controlPlane:
  architecture: amd64
  hyperthreading: Enabled
  name: master
  platform: {}
  replicas: 1
metadata:
  creationTimestamp: null
  name: lab
networking:
  clusterNetwork:
  - cidr: 10.128.0.0/14
    hostPrefix: 23
  machineNetwork:
  - cidr: 10.0.0.0/16
  networkType: OVNKubernetes
  serviceNetwork:
  - 172.30.0.0/16
platform:
  vsphere:
    apiVIPs:
    - 192.168.35.101
    failureDomains:
    - name: generated-failure-domain
      region: generated-region
      server: 192.168.11.10
      topology:
        computeCluster: /Datacenter/host/vSAN-Cluster
        datacenter: Datacenter
        datastore: /Datacenter/datastore/vsanDatastore
        networks:
        - okd
        resourcePool: /Datacenter/host/vSAN-Cluster//Resources
      zone: generated-zone
    ingressVIPs:
    - 192.168.35.102
    vcenters:
    - datacenters:
      - Datacenter
      password: VMware1!
      port: 443
      server: 192.168.11.10
      user: administrator@vsphere.local
publish: External
pullSecret: '<get this infor from redhat>'
sshKey: 'ssh-rsa AAAAB...................'
