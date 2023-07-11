# opcap-ansible
Contains Ansible playbooks for installing operators and checking status of the install.

## Usage
Set the following env vars:

```
K8S_AUTH_VERIFY_SSL=no    # If you have a self-signed cert for your cluster
K8S_AUTH_API_KEY=<snip>   # Easiest is to create a service account with cluster-admin, and pull the token from there
K8S_AUTH_HOST=https://api.my-cluster.domain:6443
```
or if you prefer set:
```
K8S_AUTH_KUBECONFIG=<path to your kubeconfig file>
```

Copy var.yaml.example to vars.yaml and modify accordingly. If packages is empty, it will pull ALL packages
from the catalog source.

`ansible-playbook -e @vars.yaml audits.yaml`

