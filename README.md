Ansible Role: teamd
===================

Configures a teamd interface based on YAML configuration.

Requirements
------------

Only tested on CentOS 7.1 x86_64.

Role Variables
--------------

This role requires that you describe the teamd interface configuration using
the same parameters required by teamd in its original JSON format, except here
you will be using YAML.

  - hosts: localhost
    become: yes
    roles:
  
      - role: teamd
        teamd_config:
          device: 'team0'
          ports:
            'enp3s0f0': {}
            'enp3s0f1': {}
          link_watch: 
            name: 'ethtool'
          runner: 
            name: 'lacp'
            active: 'yes'
            fast_rate: 'no'
            tx_hash:
              - 'eth'
              - 'ipv4'


Dependencies
------------

None.

Example Playbook
----------------

2-port LACP configuration:

    - hosts: localhost
      become: yes
      roles:

        - role: teamd
          teamd_config:
            device: 'team0'
            ports:
              'enp3s0f0': {}
              'enp3s0f1': {}
            link_watch:
              name: 'ethtool'
            runner:
              name: 'lacp'
              active: 'yes'
              fast_rate: 'no'
              tx_hash:
                - 'eth'
                - 'ipv4'
