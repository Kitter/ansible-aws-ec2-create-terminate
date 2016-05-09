## Provision with ec2 
requirements are:
- python 2.6 =>
- boto module
- aws account with aws_access_key + aws_secret_key
- aws ec2.py file under /etc/ansible/hosts and a configured ansible.cfg file 
- aws keypair to connect to aws (uploaded to aws as well as located somewhere where your ssh config can find it and use it).


## How To Example 

Using ec2 you can easily create instances, run your configuration against the newly created instances and then terminate them if you like.

### Example of creating 2 ec2 instances - tagged jenkins_master and jenkins_slave

    $ ansible-playbook   create.yml

    PLAY ***************************************************************************

    TASK [setup] *******************************************************************
    ok: [localhost]

    TASK [Launch each ec2 Instance] ************************************************
    changed: [localhost] => (item={u'volume_size': 10, u'name': u'jenkinsmaster', u'tags': {u'jenkins': u'master'}})
    changed: [localhost] => (item={u'volume_size': 15, u'name': u'jenkinsslave', u'tags': {u'jenkins': u'slave'}})
    
    ........ 

    PLAY RECAP *********************************************************************
    localhost                  : ok=4    changed=1    unreachable=0    failed=0


run your playbooks with configuration and then terminate when done.

### Example of terminating ec2 instances

    $ ansible-playbook   terminate.yml

    PLAY [Terminate instances] *****************************************************

    TASK [setup] *******************************************************************
    ok: [52.29.53.1]
    ok: [52.28.61.215]

    TASK [Terminate i-06cc2bac4ea70f44e instance in eu-central-1 with hostname ec2-52-29-53-1.eu-central-1.compute.amazonaws.com] ***
    changed: [52.28.61.215 -> localhost]
    changed: [52.29.53.1 -> localhost]

    PLAY RECAP *********************************************************************
    52.28.61.215               : ok=2    changed=1    unreachable=0    failed=0
    52.29.53.1                 : ok=2    changed=1    unreachable=0    failed=0

