# Ansible Role: Redis HA for Kubernetes

Ansible role to install Redis HA on Kubernetes.

## Role Variables

```yaml
# Image used
redis_image: quay.io/smile/redis:4.0.6r2

# Namespace
redis_namespace: default

# Number of replicas
redis_server_replicas: 3
redis_sentinel_replicas: 3

# Node selector
redis_node_selector: {}

# Resources
redis_server_resources:
  requests:
    memory: 200Mi
    cpu: 100m
  limits:
    memory: 700Mi

redis_sentinel_resources:
  requests:
    memory: 200Mi
    cpu: 100m
  limits:
    memory: 200Mi
```

## Dependencies

`kubectl` needs to be installed on the host  targeted by the role.

## Example Playbook

```yaml
- hosts: kube-master
  run_once: true
  vars:
    redis_server_replicas: 5
    redis_sentinel_replicas: 3
  roles:
    - role: redis
```

Use `run_once` to run the role on only one available master in the cluster.

## Test

```bash
pip install ansible-toolbox
ansible-role roles/redis/
```