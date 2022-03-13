# EX447
preparation for EX447 exam <br/>
The purpose is to test the different objectives covered by DO447 preparing for EX447


## Chapter 2: 
ungrouped: a generic group for hosts without groups in yml inventories<br/>
Useful commands:
```
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
- lists: max, min, sum, first, last, length, random, reverse, sort, unique, flatten, uninion, difference, intersect, ... <br/>
- dictionary: combine, dict2items, items2dict <br/>
- strings: lower, upper, capitalize, b64encode, b64decode, quote <br/>
- hash: hash, password_hash <br/>
- replace, regex_search, regex_replace <br/>
- json_query, to_json, to_yaml, to nice_json, to_nice_yaml <br/>

### lookup: