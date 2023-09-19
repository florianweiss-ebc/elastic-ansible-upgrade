# Elasticsearch Ansible Upgrade

Before starting to upgrade, replace `<USERNAME>` with username used to connect to virtual machines and `<ELASTIC_PASSWORD>` with the Elasticsearch password of the `elastic` user. Furthermore, it would be possible to overwrite the `elastic_version` in the command line. To archieve that, replace `<ELASTIC_VERSION>` with the desired version. To set it via the defaults, change the version in the `roles/upgrade_elastic_nodes/defauls/main.yml` and remove `elastic_version=<ELASTIC_VERSION>` from the `--extra-vars`. Last but not least, adapt the `inventory` file accordingly.

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
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u <USERNAME> --limit "elastic-01" --extra-vars "elastic_password=<ELASTIC_PASSWORD> elastic_version=<ELASTIC_VERSION>"
```

## Upgrade all nodes designed to run one by one and wait until health of cluster is green before process to other step
```
ansible-playbook -i inventory upgrade_elastic_nodes.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD> elastic_version=<ELASTIC_VERSION>"
```