# Elasticsearch Ansible Upgrade

Before starting to upgrade, replace `<USERNAME>` with username used to connect to virtual machines and `<ELASTIC_PASSWORD>` with the Elasticsearch password of the `elastic` user. Furthermore, adapt the `inventory` file accordingly.

## Check if hosts are reachable
```
ansible -i inventory -m ping elasticsearch -u <USERNAME>
```

## Check if Elasticsearch cluster is green
```
ansible-playbook -i inventory check_elastic_health.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD>"
```

## Upgrade all Elasticsearch nodes
This playbook is designed to run every node one by one and wait until health of cluster is green before continuing to the next node.
```
ansible-playbook -i inventory upgrade_elasticsearch.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD>"
```

## Upgrade fleet artifact registry
This playbook is used to upgrade the fleet artifact registry. To get the current cluster version for the package download, `<ELASTIC_NODE>` needs to be set to the IP or hostname of one of the Elasticsearch nodes.
```
ansible-playbook -i inventory upgrade_fleet.yml -u <USERNAME> --extra-vars "elastic_password=<ELASTIC_PASSWORD> elastic_node=<ELASTIC_NODE>"
```

## Upgrade Elastic stack component
Elastic components can be upgraded with a generic playbook, which only stops, upgraded and restarts the corresponding service.  
Example: Upgrade Kibana
```
ansible-playbook -i inventory upgrade_kibana.yml -u <USERNAME>
```