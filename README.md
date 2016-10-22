## Deploy Kubernetes HA with Ansible

### Requirements:
- Ansible 2.1.*
- Vagrant 1.8.*
- VirtualBox 5.*

### Check available hosts on vagrant:
```vagrant status```

### Run on Vagrnat:
```vagrant up <HOSTNAME>```

example:
```vagrant up docker-registry```

### Run ansible:

#### Check connection for all tests:
```ansible -i ./hosts all -m ping```

#### Limit connection test to one host:
```ansible -i ./hosts all --limit prod-docker-registry -m ping```

#### Ansible dry run:
```ansible-playbook -i ./hosts --limit docker-registry playbook.yaml --chec```

#### Run Ansible on remote host group:
```ansible-playbook -i ./hosts --limit docker-registry playbook.yaml```

- -i - file with hosts list
- --limit - run only on host from group
- playbook.yaml - playbook to run name

#### Get all facts from remote machine:
```ansible -i ./hosts all --limit prod-docker-registry -m ping```
