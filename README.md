# opcap-ansible
Contains Ansible playbooks for installing operators and checking status of the install.

## Usage

### Setup
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

Copy `var.yaml.example` to `vars.yaml` and modify accordingly. If `packages` value is empty, it will pull ALL packages from the catalog source.

### Run playbooks with Ansible Navigator

The fastest way to get started is to run the playbooks via `ansible-navigator` with an Ansible execution environment container image:

```
ansible-navigator run audits.yaml --container-engine podman --eei quay.io/opdev/opcap-ansible-ee:latest -e @vars.yaml --penv K8S_AUTH_VERIFY_SSL --penv K8S_AUTH_API_KEY --penv K8S_AUTH_HOST -m stdout
````

or if you prefer to provide a kubeconfig:

```
ansible-navigator run audits.yaml --container-engine podman --eei quay.io/opdev/opcap-ansible-ee:latest -e @vars.yaml --senv K8S_AUTH_KUBECONFIG=/dir/kubeconfig --eev /dir:/dir -m stdout
```

### Run playbooks with Ansible Playbook


You may prefer to run playbooks via `ansible-playbook` although this method requires proper dependencies installed on localhost:

```
ansible-playbook -e @vars.yaml audits.yaml
```

### Misc

Build your own execution environment image with `ansible-builder`:

```
ansible-builder build  --container-runtime=podman --tag=opcap-ansible-ee --prune-images --verbosity 3
```



