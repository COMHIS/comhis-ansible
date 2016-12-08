# Building servers

First, authenticate to Pouta. You can get the needed credentials from https://pouta.csc.fi/dashboard/project/access_and_security/api_access/openrc/ .

Then, simply run e.g. `ansible-playbook playbooks/build-frontend`. Here, the frontend node needs to be built before the others, as, being the only node with a public IP, it acts as a bastion host to access the others, which are only in a private subnet. You'll need the COMHIS RSA key.

# Tearing down servers

 * `openstack server destroy processing-ecco`
 * `openstack stack destroy frontend`
