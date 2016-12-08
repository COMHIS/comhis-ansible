# Building servers

First, authenticate to Pouta. You can get the needed credentials from https://pouta.csc.fi/dashboard/project/access_and_security/api_access/openrc/ .

Then, simple run e.g. `ansible-playbook playbooks/build-frontend`. Here, the frontend node needs to be built before the others, as, being the only node with a public IP, it acts as a bastion host to access the others, which are only in a private subnet.

# Tearing down servers

 * `openstack stack destroy processing`
 * `openstack stack destroy frontend`
