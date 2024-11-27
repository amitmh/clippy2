# clippy2

ansible elasticsearch_group -i inventory.yml -b -m lineinfile -a "
path=/etc/elasticsearch/elasticsearch.yml
regexp='^discovery\.seed_hosts:'
line='discovery.seed_hosts: {{ groups['elasticsearch_group'] | list | to_yaml }}'
state=present" 
