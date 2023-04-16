# Ansible coreos-k8s Automations

## Install requirements
Install the required dependencies (default role folder is .galaxy-roles, which is ignored):
```
ansible-galaxy install -r requirements.yaml
```

## Create and encrypt your secrets
Create a file in the project root dir named .secrets.yaml with the following command:
```
ansible-vault create .secrets.yaml
```
put the password you like (for example "test-password") and populate the file with the k8s token:
```yaml
k8s:
  token: <put-the-token-here>
```

## SETUP ENV variable for your vault password
Put your vault password in a safe place and properly populate the env variable programmatically
```
echo 'export ANSIBLE_VAULT_PASSWORD_FILE=~/.password-file' >> ~/.bashrc 
```
A more ideal solution would be to populate the encrypted .secrets.yaml or the password from a password 
manager CLI.

## Run the playbook
The available playbooks are the following:
- k8s-init: sets up kubernetes using CRIO, kube router and join the worker nodes to the control planes.
- k8s-reset: resets the cluster to allow k8s-init to run once more.
- k8s-tools-setup: Install some basic tools such as kubernetes-dashboard and helm.