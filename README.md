# EX447
preparation for EX447 exam <br/>
The purpose is to test the different objectives covered by DO447 preparing for EX447 <br/>

To use this project, please follow below steps:
- install ansible ( the code was developped using ansible 2.9 )
- install docker and docker-compose in your environment
- run the command in Dockerfile to create the customized image
- run the command in docker-compose.yml file to startup client instances
- run the command in each playbook to test the playbook


## Chapter 2: 
#### Managing inventories
ungrouped: a generic group for hosts without groups in yml inventories<br/>
Useful commands:
```bash
ansible-inventory -i inventory --list
ansible-inventory --yaml -i inventory --list > converted_inventory.yml
ansible all -i converted_inventory.yml -m ping
```
Create group_vars & host_vars folders, subfolders for groups<br/>
Special inventory vars: ansible_connection, ansible_host, ansible_port, ansible_user, ansible_become_user, ansible_python_interpreter


## Chapter 3: 
become, become_user, become_method<br/>
import_role, include_role<br/>
notify, listen <br/>
tags, skip-tags, tagged, untagged <br/>
never, always<br/>
gather_facts, forks, <br/>
SSH: ControlMaster, ControlPersist, Pipelining <br/>
Callbacks: timer, profile_tasks, profile_roles, cgroup_perf_recap <br/>
```bash
ansible-doc -lt callback
ansible-doc -t cgroup_perf_recap
sudo cgcreate -a aniskhach:aniskhach -t aniskhach:aniskhach -g cpuacct,memory,pids:ansible_profile
cgexec -g cpuacct,memory,pids:ansible_profile ansible-playbook playbook.yml
```


## Chapter 4: 
### filters:
- generic: (int, string, bool, list, ...),  mandatory, default, default(omit)<br/>
- maths: pow, log, root, abs, ...<br/>
- lists: max, min, sum, first, last, length, random, reverse, sort, unique, flatten, uninion, difference, intersect, select, ... <br/>
- dictionary: combine, dict2items, items2dict <br/>
- strings: lower, upper, capitalize, b64encode, b64decode, quote <br/>
- hash: hash, password_hash <br/>
- replace, regex_search, regex_replace <br/>
- json_query ( apt install python3-jmespath ), to_json, to_yaml, to_nice_json, to_nice_yaml <br/>

### lookups:

```bash
ansible-doc -lt lookup
ansible-doc -t lookup file
```
lookup and query: file, template, pipe, lines, env, url, k8s, password, dig ( ``` pip install  dnspython ``` ), list ... <br/>

### advanced loops:
loop instead of with_* , flatten, dict2items, fileglob, subelements

### IP addr processing:
lookup: ipaddr ( ipv4, ipv6, public, private, subnet, ...), dig, dnstxt


## Chapter 5: 
delegating tasks: delegate_to, hostvars (```hostvars['serverb']['ansible_facts']['default_ipv4']['address']```)<br/>
rolling updates: serial, max_fail_percentage, ansible_play_hosts, ansible_play_batch, run_once <br/>


## Chapter 6: 
#### Installing Tower
```bash
./setup.sh
awx-manage changepassword admin
```

## Chapter 7: 
#### Managing Users, Teams
General roles (Organization): Project Admin, Inventory Admin, Credential Admin, Notification Admin, Workflow Admin, Job Template Admin, Member, Read, Execute<br/>
User roles: System Administrator, System Auditor, Normal User<br/>
Teams roles: Admin, Member, Read <br/>
```bash
tower-cli role grant --user 'sam' --target-team 'Operators' --type 'admin'
```

## Chapter 8: 
#### Managing inventories
Inventories roles: Admin, Use, Ad Hoc, Update, Read <br/>
import an inventory from cli:<br/>
```bash
awx-manage inventory_import --inventory-name=myapp-inv --source=inventory.yml
```
Credentials: Machine, Source Control, Network, Vault, dynamic inventories (AWS, vcenter, ...), ... <br/>
Credential roles: Admin, Use, Read <br/>

## Chapter 9: 
#### Projects and Job templates
Project roles: Admin, Use, Update, Read <br/>
Job Template roles: Admin, Execute, Read <br/>


## Chapter 10: 
#### Advanced Job Workflows
Fact cache ( gather_facts: false) <br/>
Prompt on launch for variables <br/>
Job Template Surveys for extra variables <br/>
Workflow Job Templates, WORKFLOW VISUALIZER <br/>
Workflow Job Template roles: Admin, Execute, Read, Approve <br/>

## Chapter 11: 
#### REST APIs
```bash
curl -X GET https://tower-url/api/ -k
curl -X GET --user admin:password https://tower-url/api/v2/instances/ | json_pp
curl -X GET --user admin:password http://localhost/api/v2/job_templates/15/ -k -s | json_pp
curl -X POST --user admin:password http://localhost/api/v2/job_templates/15/launch/ -k -s | json_pp
curl -X GET "http://localhost/api/v2/users/"  --user admin --oauth2-bearer xdWkzTZLJoQCVHpH -k -s | json_pp
```
Create an oauth2 token:
```bash
awx-manage create_oauth2_token --user admin
```

## Chapter 12: 
#### Inventories
update inventory from CLI:

```bash
awx-manage inventory_import --inventory-name=myapp-inv --source=inventory.yml --override
```
Inventories from SCM, through projects ( Sourced from a Project ) <br/>
Smart Inventories: use filters ( like ```ansible_facts.ansible_distribution:"RedHat"``` ) <br/>