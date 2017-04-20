# Prequisites

Run ansible-galaxy install -r requirements.yml to install role dependencies.

# Building servers

First, authenticate to Pouta. You can get the needed credentials from https://pouta.csc.fi/dashboard/project/access_and_security/api_access/openrc/ .

Then, run e.g. `ansible-playbook playbooks/build-frontend.yml`. Here, the frontend node needs to be built before the others, as, being the only node with a public IP, it acts as a bastion host to access the others, which are only in a private subnet. You'll need the COMHIS RSA key. To get an SSH conf of the current servers, run `ansible-playbook playbooks/generate-ssh-config.yml`.

# Building a temporary processing node

Run `ansible-playbook playbooks/build-processing.yml -e name=[nameofnode]` for a console node (optionally adding `-e flavor=[flavor]`).

For a GUI node, run `ansible-playbook playbooks/build-processing-desktop.yml -e name=[nameofnode]`. After that, create an SSH tunnel to the node by running e.g. ` ssh -F ssh.conf -N -L 4001:[nameofnode]:4000 frontend` (add `-f` to make the SSH tunnel go to the background). After this, you can connect to the remote desktop using [NoMachine](https://www.nomachine.com/). Set `localhost` as the host and `4001` (or whatever you put into the tunnel) as the port. Select private key as the authentication method and point NoMachine to your COMHIS RSA key. The username is `cloud-user`.

# Tearing down servers

Run `ansible-playbook playbooks/delete-node.yml -e name=[nameofnode]`
