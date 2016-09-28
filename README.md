Ansible role for Pivotal tc Server

**Features**

- Compatible with RHEL 7
- Installs Pivotal tc Server
- Creates tc Server instances
- Enables tc Server instances at boot
- Supports instance-specific configurations
- Restarts tc Server instances as necessary

**Wishlist**

- Add support for RHEL 6

**Instructions**

1. Edit defaults/main.yml as desired

2. Edit tasks/configure-instances.yml as desired

3. In your playbook include the tcserver role and define any desired variables for the instances
  - Available variables:
    - `name`: The name of the instance. This is the only variable that's required.
    - `cluster_node_prefix`: The cluster node name prefix. A numerical suffix will be appended that will be unique for each server in the play. If this is not provided, clustering will not be configured.
    - `port_ajp_http`: The AJP HTTP port. If `port_ajp_https` is provided but not `port_ajp_http`, tc Server will use port 8009 by default. If neither is provided, AJP will not be configured.
    - `port_ajp_https`: The AJP HTTPS port. This can be set to the same value as `port_https` if desired. If `port_ajp_http` is provided but not `port_ajp_https`, tc Server will use port 8443 by default. If neither is provided, AJP will not be configured.
    - `port_http`: The HTTP port. If `port_https` is provided but not `port_http`, an HTTP connector will not be created. If neither is provided, tc Server will configure an HTTP connector with the default port of 8080.
    - `port_https`: The HTTPS port. If this isn't provided, an HTTPS connector will not be created.
    - `port_jmx`: The JMX port. If this isn't provided, tc Server will use port 6969 by default.
    - `tomcat_major_version:`: The Tomcat major version, either 7 or 8. If this isn't provided, tc Server will use version 8 by default.

    Sample playbook:

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
                port_jmx: 6970
                tomcat_major_version: 7
