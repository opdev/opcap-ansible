# opcap-ansible
Contains Ansible playbooks for installing operators and checking status of the install.

## Usage
Set the following env vars:

```
K8S_AUTH_VERIFY_SSL=no    # If you have a self-signed cert for your cluster
K8S_AUTH_API_KEY=<snip>   # Easiest is to create a service account with cluster-admin, and pull the token from there
K8S_AUTH_HOST=https://api.my-cluster.domain:6443
```

Look over the vars.yaml and modify accordingly. If packages is empty, it will pull ALL packages
from the catalog source.
