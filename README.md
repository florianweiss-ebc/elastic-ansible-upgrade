# Elasticsearch Ansible Upgrade

Before starting to upgrade, replace `<USERNAME>` with username used to connect to virtual machines and `<ELASTIC_PASSWORD>` with the Elasticsearch password of the `elastic` user. Furthermore, adapt the `inventory` file accordingly.

## Check if nodes are reachable
```
ansible -i inventory -m ping elasticsearch -u <USERNAME>
```

## Check if cluster health is green
```
ansible-playbook -i inventory check_elastic_health.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD>"
```

## Upgrade specific single node
```
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u <USERNAME> --limit "elastic-01" --extra-vars "elastic_password=<ELASTIC_PASSWORD>"
```

## Upgrade all nodes designed to run one by one and wait until health of cluster is green before process to other step
```
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD>"
```

# TODOs
- refactor variables to use elastic version from cluster
- refactor fleet upgrade script to ansible native
- refactor versionlocks and curls to native ansible