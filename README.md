# Elasticsearch Ansible Upgrade

Before starting to upgrade replace `my_user` with username used to connect to virtual machines. Furthermore, adapt the inventory file accordingly.  

## Check nodes
```
ansible -i inventory -m ping elasticsearch -u my_user
```

## Upgrade specific single node
```
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u my_user --limit "elastic-01"
```

## Upgrade all nodes designed to run one by one and wait until health of cluster is green before process to other step
```
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u my_user
```