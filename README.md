# opcap-ansible
Contains Ansible playbooks for installing operators and checking status of the install.

## Usage

### Setup
Set the following env vars:

```
export K8S_AUTH_VERIFY_SSL=no    # If you have a self-signed cert for your cluster
export K8S_AUTH_API_KEY=<snip>   # Easiest is to create a service account with cluster-admin, and pull the token from there
export K8S_AUTH_HOST=https://api.my-cluster.domain:6443
```
or if you prefer set:
```
export K8S_AUTH_KUBECONFIG=<path to your kubeconfig file>
```

Copy `var.yml.example` to `vars.yml` and modify accordingly. If `packages` value is empty, it will pull ALL packages from the catalog source.

### Run playbooks with Ansible Navigator

The fastest way to get started is to run the playbooks via `ansible-navigator` with an Ansible execution environment container image:

```
ansible-navigator run audits.yml --container-engine podman --eei quay.io/opdev/opcap-ansible-ee:latest -e @vars.yml --penv K8S_AUTH_VERIFY_SSL --penv K8S_AUTH_API_KEY --penv K8S_AUTH_HOST -m stdout
````

or if you prefer to provide a `kubeconfig`:

```
ansible-navigator run audits.yml --container-engine podman --eei quay.io/opdev/opcap-ansible-ee:latest -e @vars.yml --senv K8S_AUTH_KUBECONFIG=/dir/kubeconfig --eev /dir:/dir -m stdout
```

## Development

### Create a Python Virtual Environment

To avoid global installation of Python packages, we recommend a Python virtual environment to install all required dependencies and to run all Ansible-related tools:

```
python -m venv opcap-ansible
source opcap-ansible/bin/activate
pip install -r requirements.txt
```

To leave your virtual environment:

```
deactivate
```

### Run playbooks with Ansible Playbook


You can quickly run playbooks within your Python virtual environment:

```
ansible-playbook -e @vars.yml audits.yml
```


### Build a new execution environment image

If you add dependencies, you may want to build and test a new execution environment image:

```
ansible-builder build  --container-runtime=podman --tag=opcap-ansible-ee --prune-images --verbosity 3
```

### Misc

* Filenames should use the `.yml` suffix in favor of `.yaml`
