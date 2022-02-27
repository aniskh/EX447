# EX447
preparation for EX447 exam
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
