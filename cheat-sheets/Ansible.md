### config

ansible -i <hostfile> --list-hosts all  # list all configure hosts, hostfile can be different from /etc/ansible/hosts



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

### Remote Execution

    ansible all -m ping

Execute arbitrary commands

    ansible <hostgroup> -a <command>
    ansible all -a "ifconfig -a"
	ansible <hostgroup>  -s -m <module> -a <command> # excute module command with sudo privilege

### Debugging

List facts and state of a host

    ansible <host> -m setup                            # All facts for one host
    ansible <host> -m setup -a 'filter=ansible_eth*'   # Only ansible fact for one host
    ansible all -m setup -a 'filter=facter_*'          # Only facter facts but for all hosts

Save facts to per-host files in /tmp/facts

    ansible all -m setup --tree /tmp/facts

