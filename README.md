# Oracle installation
This playbook provides an automated way of Oracle 12C installation. Please note, it is a modified version of [cvezalis/oracledb-ansible](https://github.com/cvezalis/oracledb-ansible).


## Prerequisities
* **OS RH/CentOS** 
* **Files - host, ansible.cfg**
    * You will likely run the playbook against different host than a VM created by Vagrant. In such case, amend both files accordingly (username, public key, hostname).
* **Copy ssh public key to target machine**
* **Enable passwordless sudo**
    * E.g. add new file to /etc/sudoers.d/<YOUR FILE> with content  <YOUR USER NAME> ALL=(ALL) NOPASSWD: ALL
* **Oracle 12C installer** 
    * The project does not contain zip files. You have to download installer archives at Oracle site
    * Once obtained, please copy them to *roles/install-oracle/files* as *linuxamd64_12102_database_1of2.zip* and *linuxamd64_12102_database_2of2.zip*
* **Oracle SqlPlus installer**
  * The project does not contain installation RPM files. You have to download RPM files for SqlPlus at Oracle site
    * Once obtained, please copy it to *roles/install-sqlplus/files* as *oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm* and *oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm*

## Roles
We split the installation into several roles

Each role deals with particular responsibility.

At the moment, playbook contains following roles:
* **prepare-oracle-env**
    * This role tweaks OS, prepares directory structure for the Weblogic installation. Next to directories creation, it also copies installation related files (installer, oraInst etc). 
* **install-oracle**
    * This role installs Oracle (including listener configuration, tabase creation etc)
* **install-sqlplus**
    This role installs sqlplus client
* **run-init-script**
    * This role runs init script that creates a *appdeploy* user

## Customization
There are two YML files that enable us to tweak various bits
### infra-vars.yml
This files contains infra related variables. It covers things such as username/password, groups, paths etc.

If you need to change SID, OS user password, charset etc, this file is the right place.

### db-vars.yml
This files aims at Oracle password, Oracle installation folder and server hostname.


## Vagrant
You can run this project contains also against VM prepared by Vagrant that is included.

### Steps
* Create environment
    * ``$ vagrant up``
* Halt environment
    * ``$ vagrant halt``
* Destroy environment
    * ``$ vagrant destroy``
* Connect to environment
    * ``$ vagrant ssh``

Vagrant configuration creates a Centos/7 VM with IP address 192.168.56.13.

Please note that the Vagrant does not start deliberatelly Ansible playbook.

Though, once you create VM, you can execute the playbook manually.
``$ ansible-playbook oracle-db.yml``


Once playbook execution completes successfully, you can access Oracle Enterprise Manager at http://192.168.56.13:5500/em using following credentials:
* **user** *sys*
* **password** *oracle*

Or you connect via SSH to VM and execute following command
``$ sqlplus sys as sysdba``

Or you can connect from SQL client via JDBC connection string
``jdbc:oracle:thin:@//<IP OR HOSTNAME>:1521/orcl.oradb3.private`` with *appdeploy/appdeploy*

