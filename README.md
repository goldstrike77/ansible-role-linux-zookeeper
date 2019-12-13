![](https://img.shields.io/badge/Ansible-zookeeper-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_zookeeper.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Zookeeper Versions](#zookeeper-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs apache Zookeeper on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Zookeeper versions

The following list of supported the zookeeper releases:

* Apache Zookeeper 3.5.6

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `zoo_version`: Specify the Zookeeper version.
* `zoo_cluster`: Cluster name of servers that implements distribution performance.
* `zoo_path`: Specify the Zookeeper working directory.
* `zoo_java_home`: Environment variable to point to an installed JDK.

##### JVM memory Variables
* `zoo_jvm_xmx`: Size of the heap in MB.

##### ACL Variables
* `zoo_enable_auth`: Whether enable quorum authentication using SASL.
* `zoo_user_super_passwd`: # Administrator priviledges user password.
* `zoo_user_client_arg`: # Client authentication information.

##### Service Mesh
* `environments`: Define the service environment.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

##### Listen port
* `zoo_port.admin`: The port the embedded Jetty server listens on.
* `zoo_port.client`: Client Port.
* `zoo_port.jmx`: Prometheus jmx_exporter listens.
* `zoo_port.leader`: Leader communication.
* `zoo_port.election`: Leader election.

##### System Variables
* `zoo_arg.admin_enableServer`: Whether enable the Admin Server.
* `zoo_arg.admin_commandURL`: The URL for listing and issuing commands relative to the root URL.
* `zoo_arg.connections`: The maximum number of client connections.
* `zoo_arg.user`: Zookeeper running user.
* `zoo_arg.ulimit_nofile`: The number of files launched by systemd.
* `zoo_arg.ulimit_nproc`: The number of processes launched by systemd.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
There are no dependencies on other roles.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' zoo_version='3.5.6'

### Vars in role configuration
Including an example of how to use your role for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-zookeeper
           zoo_version: '3.5.6'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    zoo_version: '3.5.6'
    zoo_cluster: 'zk-cluster01'
    zoo_path: '/data'
    zoo_java_home: '/usr/lib/jvm/java'
    zoo_jvm_xmx: '2048'
    zoo_enable_auth: true
    zoo_user_super_passwd: 'changeme'
    zoo_user_client_arg:
      - user: 'kafka'
        passwd: 'changeme'
    zoo_port:
      admin: '18080'
      client: '2181'
      leader: '2888'
      election: '3888'
      jmx: '9405'
    zoo_arg:
      admin_enableServer: true
      admin_commandURL: '/commands'
      connections: '1000'
      user: 'zookeeper'
      ulimit_nofile: '10240'
      ulimit_nproc: '10240'
    environments: 'Development'
    tags:
      subscription: 'default'
      owner: 'nobody'
      department: 'Infrastructure'
      organization: 'The Company'
      region: 'IDC01'
    exporter_is_install: false
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_http_port: '8500'
    consul_public_clients:
      - '127.0.0.1'

## License

![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
