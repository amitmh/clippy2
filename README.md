# clippy2

ansible elasticsearch_group -i inventory.yml -b -m lineinfile -a "
path=/etc/elasticsearch/elasticsearch.yml
regexp='^discovery\.seed_hosts:'
line='discovery.seed_hosts: {{ groups['elasticsearch_group'] | list | to_yaml }}'
state=present" 


ansible elasticsearch_group -i inventory.yml -b -m shell -a "
hosts=\$(printf ',\"%s\"' {{ groups['elasticsearch_group'] | join(' ') }});
hosts=\${hosts:1};
sed -i '/^discovery\.seed_hosts:/c\\discovery.seed_hosts: [\${hosts}]' /etc/elasticsearch/elasticsearch.yml"
