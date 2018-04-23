### installation
On Fedora:

	$ sudo dnf install ansible
On RHEL and CentOS:

	$ sudo yum install ansible
On Ubuntu:

	$ sudo apt-get update
	$ sudo apt-get install software-properties-common
	$ sudo apt-add-repository ppa:ansible/ansible
	$ sudo apt-get update
	$ sudo apt-get install ansible
### Inventory files
'INI-file' structure, blocks define groups.
 Hosts allowed in more than one group. Non-standard SSH port can follow hostname separated by ':'.
System default inventory is /etc/ansible/hosts, this value can be changed using -i / --inventory option or in the configuration file.

- Hostname ranges: server[01:20].example.com, db-[a:f].example.com
- Nested Groups: new group north-america containing all members of included groups
        [usa]
        hostserver1
        hostserver2
        [canada]
        hostserver2
        hostserver3
        [north-america:children]
        usa
        canada

 - list all configure hosts or hosts in the group "group_name", hostfile can be different from /etc/ansible/hosts
        $ ansible -i <hostfile> --list-hosts all/<group_name>  

### Configuration file

Configuration file precedence is as follow:
- $ANSIBLE_CONFIG
- ./ansible.cfg
- ~/.ansible.cfg
- /etc/ansible/ansible.cfg

To check which configuration file is being used, run

    $  ansible --version
    or use the -v option when executing an asnible command:
    $  ansible servers --list-hosts -v
    
### Ad Hoc command

    $ ansible host-pattern -m module [ -a 'module argument'] [-i inventopry]
where host-pattern:
- all (or *)
- hostname: foo.example.com
- groupname: webservers
- or: webservers:dbserver
- exclude: webserver:!phoenix
- intersection: webservers:&staging
- Operators can be chained: webservers:dbservers:&staging:!phoenix
- Patterns can include variable substitutions: {{foo}}, wildcards: *.example.com or 192.168.1.*, and regular expressions: ~(web|db).*\.example\.com

Ansible provides hundreds of modules

    $ ansible-doc -l             # lists all the modules that are installed in the system
    $ ansible-doc <module_name>  #view the documentaion og the module <module_name>

Execute arbitrary commands

    $ ansible all -m ping
    $ ansible <hostgroup> -a <command>
    $ ansible all -a "ifconfig -a"
	$ ansible <hostgroup>  -s -m <module> -a <command> # excute module command with sudo privilege
	
### Playbooks

    ansible-playbook <YAML>                   # Run on all hosts defined
    ansible-playbook <YAML> -f 10             # Run 10 hosts parallel
    ansible-playbook <YAML> --verbose         # Verbose on successful tasks
    ansible-playbook <YAML> -C                # Test run
    ansible-playbook <YAML> -C -D             # Dry run
    ansible-playbook <YAML> -l <host>         # Run on single host
	ansible-playbook <YAML> --extra-vars "var1=value1 var2=value2 ..." #Run with variable substituion

Run Infos

    ansible-playbook <YAML> --list-hosts
    ansible-playbook <YAML> --list-tasks

Syntax Check

    ansible-playbook --syntax-check <YAML>

### Debugging

List facts and state of a host

    ansible <host> -m setup                            # All facts for one host
    ansible <host> -m setup -a 'filter=ansible_eth*'   # Only ansible fact for one host
    ansible all -m setup -a 'filter=facter_*'          # Only facter facts but for all hosts

Save facts to per-host files in /tmp/facts

    ansible all -m setup --tree /tmp/facts
