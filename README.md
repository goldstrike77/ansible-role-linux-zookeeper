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
* `zoo_path`: Specify the Zookeeper working directory.
* `zoo_java_home`: Environment variable to point to an installed JDK.

##### JVM memory Variables
* `zoo_jvm_metaspace`: Size of the metaspace in MB.
* `zoo_jvm_xmn`: Size of the heap for the young generation in MB.
* `zoo_jvm_xmx`: Size of the heap in MB.
* `zoo_jvm_xss`: Size of thread stack in KB.

##### Service Mesh
* `environments`: Define the service environment.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: false Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

##### Syslog parameters
* `syslog`: A boolean value, Enable or Disable send console and access log to remote Syslog server.
* `syslog_port`: Syslog server port.
* `syslog_protocol`: Syslog server protocol.
* `syslog_server`: List of syslog server list.

##### Listen port
* `zoo_port.admin`: The port the embedded Jetty server listens on.
* `zoo_port.client`: Client Port.
* `zoo_port.jmx`: Prometheus jmx_exporter listens.
* `zoo_port.wrapper`: A socket to communicate with its Java component running inside a JVM.
* `zoo_port.wrapper_jvm`: A socket to communicate with its Java component running inside a JVM.

##### System Variables
* `zoo_arg.admin_enableServer`: Whether enable the Admin Server.
* `zoo_arg.admin_commandURL`: The URL for listing and issuing commands relative to the root URL.
* `zoo_arg.connections`: The maximum number of client connections.
* `zoo_arg.jvm_heapdumppath`: Heap dump folder.
* `zoo_arg.jvm_security_egd`: Random number generation library.
* `zoo_arg.lc_ctype`: The language of messages.
* `zoo_arg.timezone`: Default timezone for a single instance of a running JVM.
* `zoo_arg.user`: Zookeeper running user.
* `zoo_arg.ulimit_core`: The number of core dump launched by systemd.
* `zoo_arg.ulimit_nofile`: The number of files launched by systemd.
* `zoo_arg.ulimit_nproc`: The number of processes launched by systemd.
* `zoo_arg.wrapper_console_format`: Format to use for output to the console.
* `zoo_arg.wrapper_console_loglevel`: Log level to use for console output.
* `zoo_arg.wrapper_java_command_loglevel`: Log level to use for Java command.
* `zoo_arg.wrapper_logfile`: Sets the path to the Wrapper log file.
* `zoo_arg.wrapper_logfile_format`: Format to use for logging to the log file.
* `zoo_arg.wrapper_logfile_loglevel`: Filters messages sent to the log file according to their log levels.
* `zoo_arg.wrapper_logfile_maxfiles`: Controls the maximum number of rolled files.
* `zoo_arg.wrapper_logfile_maxsize`: Controls the maximum size of rolled files.
* `zoo_arg.wrapper_syslog_loglevel`: Log level to use for logging to the Event Log on syslog on UNIX systems.
* `zoo_arg.wrapper_ulimit_loglevel`: Controls at which log level resource limits will be logged.

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
    zoo_path: '/data'
    zoo_java_home: '/usr/lib/jvm/java'
    zoo_jvm_metaspace: '512'
    zoo_jvm_xmn: '384'
    zoo_jvm_xmx: '2048'
    zoo_jvm_xss: '256'
    zoo_port:
      admin: '18080'
      client: '2181'
      jmx: '9405'
      wrapper: '33000-33999'
      wrapper_jvm: '34000-34999'
    zoo_arg:
      admin_enableServer: true
      admin_commandURL: '/commands'
      connections: '1000'
      jvm_heapdumppath: '/tmp'
      jvm_security_egd: '/dev/urandom'
      lc_ctype: 'zh_CN.UTF-8'
      timezone: 'Asia/Shanghai'
      user: 'zookeeper'
      ulimit_core: 'unlimited'
      ulimit_nofile: '10240'
      ulimit_nproc: '10240'
      wrapper_console_format: 'PM'
      wrapper_console_loglevel: 'INFO'
      wrapper_java_command_loglevel: 'NONE'
      wrapper_logfile: 'zookeeper.out'
      wrapper_logfile_format: 'ZM'
      wrapper_logfile_loglevel: 'INFO'
      wrapper_logfile_maxfiles: '25'
      wrapper_logfile_maxsize: '50m'
      wrapper_syslog_loglevel: 'NONE'
      wrapper_ulimit_loglevel: 'STATUS'
    syslog: false
    syslog_port: '12201'
    syslog_protocol: 'udp'
    syslog_server:
      - '127.0.0.1'
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
