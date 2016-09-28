Ansible role for Pivotal tc Server

**Features**

- Currently tested with RHEL 7
- Installs Pivotal tc Server
- Creates tc Server instances
- Enables tc Server instances at boot
- Copies instance-specific configuration files (or defaults)
- Restarts tc Server instances as necessary

**Wishlist**

- Add support for RHEL 6

**Instructions**

1. Edit defaults/main.yml as desired

2. Include the tcserver role and define any desired variables for the instances

        ---
        - hosts: tcserver-servers
          roles:
            - { role: tcserver }
          vars:
            tcserver_instances:
              - name: instance1
                port_https: 8443
              - name: instance2
                cluster_node_prefix: instance2
                port_ajp_http: 8010
                port_ajp_https: 8444
                port_http: 8081
                port_https: 8444
                port_jmx: 6971
                tomcat_major_version: 7

3. Customize the instance files to manage

  1. Edit tasks/configure-instances.yml
  
  2. Put the files in files/templates as needed
