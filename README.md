Logserver deployment
=========

Role that install [Logserver](https://github.com/Ambisafe/ansible-role-tf-logserver) onto aws

Role Variables
--------------

-  `aws_access_key:` access key for AWS
-  `aws_secret_key:` secret key for AWS
-  `aws_region:` region for AWS
-  `aws_vpc:` VPC Name
-  `aws_subnet_id:` VPC Subnet ID for the Elasticsearch domain endpoint to be created in.
-  `aws_cidr_block_from_port_80:`

-  `ec2_name:` uniquie identifier for proxy logserver
-  `ec2_instance_type:` instance type to use for proxy logserver
-  `ec2_ami:` The ID of the AMI with which the instance was launched

-  `es_domain_name:` unique identifier for the domain.
-  `es_version:` elasticsearch version
-  `es_instance_count:` number of instances in the cluster elasticsearch.
-  `es_instance_type:` elasticsearch instance type to use for data nodes.
-  `es_volume_size:` size in GB of EBS volume to attach to each node and use for data storage.  If this parameter is set to 0 (the default), nodes will use instance storage.

Example Playbook
----------------
requirements.txt

```
  - name: logserver deployment
    src: git@github.com:Ambisafe/ansible-role-tf-logserver.git
    scm: git
    version: master
```

playbook.yml

```
- name: testing role ansible-role-tf-logserver
  hosts: localhost
  gather_facts: false
  vars:
    aws_access_key : "XXXXXXXXXXXX"
    aws_secret_key : "XXXXXXXXXXXX"
    aws_region : "eu-west-1"
    aws_vpc : "vpc-0000000"
    aws_subnet_id: "subnet-0000000"
    aws_cidr_block_from_port_80: "0.0.0.0/0"

    ec2_name: "logserver-proxy"
    ec2_instance_type: "t2.nano"
    ec2_ami: "ami-0000000"


    es_domain_name: "elasticsearch_cluster"
    es_version: "6.0"
    es_instance_count: "1"
    es_instance_type: "t2.small.elasticsearch"
    es_volume_size: "10"
  roles:
       - { role: aansible-role-tf-logserver }
```

Author Information
------------------
Artem Yushkov

DevOps@Ambisafe
