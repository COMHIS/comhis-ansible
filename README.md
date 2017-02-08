# Building servers

First, authenticate to Pouta. You can get the needed credentials from https://pouta.csc.fi/dashboard/project/access_and_security/api_access/openrc/ .

Then, simply run e.g. `ansible-playbook playbooks/build-frontend.yml` or `ansible-playbook playbooks/build-internal.yml -e "name=processing-ecco" -e "flavor=io.700GB" -e "group=processing";ansible-playbook playbooks/configure-processing.yml -e "name=processing-ecco";ansible-playbook playbooks/configure-ecco-data.yml -e "name="processing-ecco"`. Here, the frontend node needs to be built before the others, as, being the only node with a public IP, it acts as a bastion host to access the others, which are only in a private subnet. You'll need the COMHIS RSA key.

# Tearing down servers

 * `openstack server delete processing-ecco`
 * `openstack server delete frontend`
