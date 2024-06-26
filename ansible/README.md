# Collection of Ansible playbooks

This directory contains a collection of Ansible playbooks that can be used to provision and configure different environments.

## Playbooks

### Kubernetes related playbooks (`k8s`)

* `k8s-kind-with-ingress` - Sets up a Kubernetes cluster using [kind](https://kind.sigs.k8s.io/) and installs [nginx-ingress](https://kubernetes.github.io/ingress-nginx/) on it
* (**WIP**)`k8s-prometheus` - Installs [Prometheus](https://prometheus.io/) on a Kubernetes cluster

## Configuration

Variables used by Ansible playbooks are stored under appropiate directories at the following path: `ansible/enviroments`. Their structure is as follows:

* `ansible/environments/<ENVIRONMENT>/group_vars/all.yml`: Variables that apply to all hosts in the environment
* `ansible/environments/<ENVIRONMENT>/host_vars/<hostname>.yml`: Variables that apply to a specific host in the environment
* `ansible/environments/<ENVIRONMENT>/group_vars/<groupname>.yml`: Variables that apply to a specific group of hosts in the environment

Any playbook applied from any of the subdirectories of `ansible/` has to be run with `-i ${OPERATIONS_DIR}/ansible/environments/<ENVIRONMENT>` flag to ensure that the correct variables are used.

Example:

```bash
  cd ./<section>/<playbook>
  ansible-playbook -i ${OPERATIONS_DIR}/ansible/environments/<ENVIRONMENT> <playbook>.yml <playbook>.yml
```

## Wizard

A `wizard.py` Typer CLI application is provided to help with the creation of new playbooks. It can be run with the following command:

```bash
  wizard.py [command]
```

The following commands are available:

* `playbook` - Creates a new playbook
* `role` - Creates a new role

Type `wizard.py [command] --help` for more information on each command.
