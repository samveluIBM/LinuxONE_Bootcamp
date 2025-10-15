# Linux Usage Lab

## Overview
 
In this lab we will be performing some basic Red Hat Linux commands on the provisioned server from the previous lab to get familiarize yourself with a Linux environment. 

1. Clone the MongoDB git repository
2. Run the setup script 
3. Run the ansible playbook 


### MongoDB installation steps
#### Clone the mongoDB git repository
Make sure you are connected to the Linux guest from the previous step.

???- example "The following is an example where the terminal will show that you are connected to the Linux guest [click to expand me]"

      ```
      
      login as: cecuser
      Pre-authentication banner message from server:
      |
      | ______________________________________________________________________
      |
      |                     Welcome to IBM Technology Zone
      | ______________________________________________________________________
      |
      |
      | IBM's internal systems must only be used for conducting IBM's business
      | or for purposes authorized by IBM management.  Use is subject to audit
      | at any time by IBM management.
      |
      | Unauthorized access will be investigated and penalties will be pursued
      | in conformance with applicable laws and regulations. If you are not an
      | authorized user disconnect now.
      |
      |
      End of banner message from server
      cecuser@129.40.60.161's password:

      ______________________________________________________________________

                        Welcome to IBM Technology Zone
      ______________________________________________________________________


      IBM's internal systems must only be used for conducting IBM's business
      or for purposes authorized by IBM management.  Use is subject to audit
      at any time by IBM management.

      Unauthorized access will be investigated and penalties will be pursued
      in conformance with applicable laws and regulations. If you are not an
      authorized user disconnect now.
      ______________________________________________________________________

      IaaS Red Hat Enterprise Linux 8.10

      Activate the web console with: systemctl enable --now cockpit.socket

      Register this system with Red Hat Insights: insights-client --register
      Create an account or view all your systems at https://red.ht/insights-dashboard
      Last login: Thu Mar 13 10:18:51 2025 from 9.19.184.79
      [cecuser@p1243-zvm1 ~]$

      ```

Enter the following Linux commands to switch to **super user** for installation and then change the directory to a temporary working directory **/tmp** .

``` bash
   sudo -i 
   cd /tmp
```

???- example "The following is an example where the terminal will show that you are connected to the Linux terminal as “root” and the working directory is tmp [click to expand me]"

      ```
      [cecuser@p1243-zvm1 /]$    sudo -i
      [root@p1243-zvm1 ~]#    cd /tmp
      [root@p1243-zvm1 tmp]#

      ```
Enter the following Linux command to install  **git** module which is needed for our MongoDB installation. For **If this ok [y/N]:** prompt answer **y**

``` bash
   yum install git
```

???- example "The following is an example where the terminal will show that you have successfully installed **git** module [click to expand me]"

      ```
      [root@itzvsi-pvsbiee ~]# yum install git
      Updating Subscription Management repositories.
      Last metadata expiration check: 0:15:37 ago on Tue Oct 14 16:32:05 2025.
      Dependencies resolved.
      ====================================================================================================
      Package              Arch       Version                  Repository                           Size
      ====================================================================================================
      Installing:
      git                  s390x      2.47.3-1.el9_6           rhel-9-for-s390x-appstream-rpms      51 k
      Installing dependencies:
      emacs-filesystem     noarch     1:27.2-14.el9_6.2        rhel-9-for-s390x-appstream-rpms     8.9 k
      git-core             s390x      2.47.3-1.el9_6           rhel-9-for-s390x-appstream-rpms     4.6 M
      git-core-doc         noarch     2.47.3-1.el9_6           rhel-9-for-s390x-appstream-rpms     3.0 M
      perl-DynaLoader      s390x      1.47-481.1.el9_6         rhel-9-for-s390x-appstream-rpms      25 k
      perl-Error           noarch     1:0.17029-7.el9          rhel-9-for-s390x-appstream-rpms      46 k
      perl-File-Find       noarch     1.37-481.1.el9_6         rhel-9-for-s390x-appstream-rpms      25 k
      perl-Git             noarch     2.47.3-1.el9_6           rhel-9-for-s390x-appstream-rpms      38 k
      perl-TermReadKey     s390x      2.38-11.el9              rhel-9-for-s390x-appstream-rpms      39 k
      perl-lib             s390x      0.65-481.1.el9_6         rhel-9-for-s390x-appstream-rpms      14 k

      Transaction Summary
      ====================================================================================================
      Install  10 Packages

      Total download size: 7.9 M
      Installed size: 40 M
      Is this ok [y/N]: y
      Downloading Packages:
      (1/10) : emacs-filesystem-27.2-14.el9_6.2.noarch.rpm                 119 kB/s | 8.9 kB     00:00
	(2/10): perl-Error-0.17029-7.el9.noarch.rpm                         605 kB/s |  46 kB     00:00
	(3/10): perl-TermReadKey-2.38-11.el9.s390x.rpm                      443 kB/s |  39 kB     00:00
	(4/10): git-core-2.47.3-1.el9_6.s390x.rpm                            75 MB/s | 4.6 MB     00:00
	(5/10): git-2.47.3-1.el9_6.s390x.rpm                                786 kB/s |  51 kB     00:00
	(6/10): git-core-doc-2.47.3-1.el9_6.noarch.rpm                       48 MB/s | 3.0 MB     00:00
	(7/10): perl-DynaLoader-1.47-481.1.el9_6.s390x.rpm                  1.3 MB/s |  25 kB     00:00
	(8/10): perl-lib-0.65-481.1.el9_6.s390x.rpm                         1.0 MB/s |  14 kB     00:00
	(9/10): perl-File-Find-1.37-481.1.el9_6.noarch.rpm                  447 kB/s |  25 kB     00:00
	(10/10): perl-Git-2.47.3-1.el9_6.noarch.rpm                         388 kB/s |  38 kB     00:00
	----------------------------------------------------------------------------------------------------
	Total                                                                33 MB/s | 7.9 MB     00:00
	Running transaction check
	Transaction check succeeded.
	Running transaction test
	Transaction test succeeded.
	Running transaction
  		Preparing        :                                                                            1/1
  		Installing       : git-core-2.47.3-1.el9_6.s390x                                             1/10
  		Installing       : git-core-doc-2.47.3-1.el9_6.noarch                                        2/10
  		Installing       : perl-lib-0.65-481.1.el9_6.s390x                                           3/10
  		Installing       : perl-File-Find-1.37-481.1.el9_6.noarch                                    4/10
  		Installing       : perl-DynaLoader-1.47-481.1.el9_6.s390x                                    5/10
  		Installing       : perl-TermReadKey-2.38-11.el9.s390x                                        6/10
  		Installing       : emacs-filesystem-1:27.2-14.el9_6.2.noarch                                 7/10
  		Installing       : perl-Error-1:0.17029-7.el9.noarch                                         8/10
  		Installing       : git-2.47.3-1.el9_6.s390x                                                  9/10
  		Installing       : perl-Git-2.47.3-1.el9_6.noarch                                           10/10
  		Running scriptlet: perl-Git-2.47.3-1.el9_6.noarch                                           10/10
  		Verifying        : perl-Error-1:0.17029-7.el9.noarch                                         1/10
  		Verifying        : perl-TermReadKey-2.38-11.el9.s390x                                        2/10
  		Verifying        : emacs-filesystem-1:27.2-14.el9_6.2.noarch                                 3/10
  		Verifying        : git-2.47.3-1.el9_6.s390x                                                  4/10
  		Verifying        : git-core-2.47.3-1.el9_6.s390x                                             5/10
  		Verifying        : git-core-doc-2.47.3-1.el9_6.noarch                                        6/10
  		Verifying        : perl-Git-2.47.3-1.el9_6.noarch                                            7/10
  		Verifying        : perl-DynaLoader-1.47-481.1.el9_6.s390x                                    8/10
  		Verifying        : perl-File-Find-1.37-481.1.el9_6.noarch                                    9/10
  		Verifying        : perl-lib-0.65-481.1.el9_6.s390x                                          10/10
		Installed products updated.

	Installed:
  	emacs-filesystem-1:27.2-14.el9_6.2.noarch            git-2.47.3-1.el9_6.s390x
  	git-core-2.47.3-1.el9_6.s390x                        git-core-doc-2.47.3-1.el9_6.noarch
  	perl-DynaLoader-1.47-481.1.el9_6.s390x               perl-Error-1:0.17029-7.el9.noarch
  	perl-File-Find-1.37-481.1.el9_6.noarch               perl-Git-2.47.3-1.el9_6.noarch
  	perl-TermReadKey-2.38-11.el9.s390x                   perl-lib-0.65-481.1.el9_6.s390x

	Complete!
      ```

We have created an Ansible playbook repository to install MongoDB on a Red Hat Linux guest and clone that repository using the following command.

``` bash
   git clone https://github.com/samveluIBM/MongoDB-Wildfire-Workshop
```

???- example "The following example shows the output of succesful cloning of the repository [click to expand me]"

      ```
      [root@p1243-zvm1 tmp]#    git clone https://github.com/samveluIBM/MongoDB-Wildfire-Workshop
      Cloning into 'MongoDB-Wildfire-Workshop'...
      remote: Enumerating objects: 20, done.
      remote: Counting objects: 100% (20/20), done.
      remote: Compressing objects: 100% (14/14), done.
      remote: Total 20 (delta 1), reused 3 (delta 0), pack-reused 0 (from 0)
      Receiving objects: 100% (20/20), 4.99 KiB | 4.99 MiB/s, done.
      Resolving deltas: 100% (1/1), done.
      [root@p1243-zvm1 tmp]#

      ```
#### Run the setup script
This step will install the python and ansibles to use ansible playbooks to install MongoDB on the Linux guest. 
Change to the cloned directory and then run the **setup** script.
Use the following commands:

``` bash
   cd MongoDB-Wildfire-Workshop/
```

``` bash
    ./setup.sh
```
???- example "The following example shows the output of succesful execution of setup.sh script [click to expand me]"

      ```
      Installed products updated.

      Installed:
      ansible-9.2.0-1.el8.noarch
      ansible-core-2.16.3-2.el8.s390x
      python3-jmespath-0.9.0-11.el8.noarch
      python3.12-3.12.8-1.el8_10.s390x
      python3.12-cffi-1.16.0-2.el8.s390x
      python3.12-cryptography-41.0.7-1.el8.s390x
      python3.12-libs-3.12.8-1.el8_10.s390x
      python3.12-pip-wheel-23.2.1-4.el8.noarch
      python3.12-ply-3.11-2.el8.noarch
      python3.12-pycparser-2.20-2.el8.noarch
      python3.12-pyyaml-6.0.1-2.el8.s390x
      python39-3.9.20-1.module+el8.10.0+22342+478c159e.s390x
      python39-libs-3.9.20-1.module+el8.10.0+22342+478c159e.s390x
      python39-pip-20.2.4-9.module+el8.10.0+21329+8d76b841.noarch
      python39-pip-wheel-20.2.4-9.module+el8.10.0+21329+8d76b841.noarch
      python39-setuptools-50.3.2-6.module+el8.10.0+22183+c898c0c1.noarch
      python39-setuptools-wheel-50.3.2-6.module+el8.10.0+22183+c898c0c1.noarch
      sshpass-1.09-4.el8.s390x

      Complete!
      [root@p1243-zvm1 MongoDB-Wildfire-Workshop]#

      ```
#### Run the ansible playbook
In this step we will run the ansible playbook to install MongoDB. Use the following command:

``` bash
   ansible-playbook mongodb8Install.yml 
```

???- example "The following example shows the output of succesful MongoDB installtion [click to expand me]"

      ```
      [root@zdblab05 zmongodb]# ansible-playbook mongodbInstall.yml

      PLAY [Install MongoDB on a Linux Guest.] ***********************************************************

      TASK [Gathering Facts] *****************************************************************************
      ok: [127.0.0.1]

      TASK [Create repo file for mongodb-enterprise] *****************************************************
      ok: [127.0.0.1]

      TASK [Install  mongodb-enterprise.] ****************************************************************
      changed: [127.0.0.1] => (item={'pkg': 'mongodb-enterprise', 'when': True})
      ok: [127.0.0.1] => (item={'pkg': 'libselinux-utils', 'when': "db_path != '/var/lib/mongodb' or log_file != '/var/log/mongodb/mongod.log'"})
      ok: [127.0.0.1] => (item={'pkg': 'policycoreutils-python-utils', 'when': "db_path != '/var/lib/mongodb' or log_file != '/var/log/mongodb/mongod.log'"})

      TASK [Set SELinux to Permissive mode.] *************************************************************
      skipping: [127.0.0.1]

      TASK [Disable SELinux permanently in configuration.] ***********************************************
      skipping: [127.0.0.1]

      TASK [Ensure db and log files exist and are owned by mongod user.] *********************************
      changed: [127.0.0.1] => (item={'path': '/var/lib/mongodb', 'state': 'directory', 'recurse': True})
      changed: [127.0.0.1] => (item={'path': '/var/log/mongodb/mongod.log', 'state': 'touch', 'recurse': False})

      TASK [Change db and/or log file paths.] ************************************************************
      changed: [127.0.0.1] => (item={'key': 'dbPath', 'value': '/var/lib/mongodb', 'when': "db_path != '/var/lib/mongodb'"})
      ok: [127.0.0.1] => (item={'key': 'path', 'value': '/var/log/mongodb/mongod.log', 'when': "log_file != '/var/log/mongodb/mongod.log'"})

      TASK [Start mongod service.] ***********************************************************************
      changed: [127.0.0.1]

      TASK [Check mongod status.] ************************************************************************
      changed: [127.0.0.1]

      TASK [Print mongod status.] ************************************************************************
      ok: [127.0.0.1] =>
      msg: |-
      ● mongod.service - MongoDB Database Server
       Loaded: loaded (/usr/lib/systemd/system/mongod.service; enabled; vendor preset: disabled)
       Active: active (running) since Mon 2025-03-10 21:51:38 UTC; 288ms ago
         Docs: https://docs.mongodb.org/manual
      Main PID: 490438 (mongod)
       Memory: 70.3M
       CGroup: /system.slice/mongod.service
               └─490438 /usr/bin/mongod -f /etc/mongod.conf

      Mar 10 21:51:38 zdblab05 systemd[1]: Started MongoDB Database Server.
      Mar 10 21:51:38 zdblab05 mongod[490438]: {"t":{"$date":"2025-03-10T21:51:38.431Z"},"s":"I",  "c":"CONTROL",  "id":7484500, "ctx":"main","msg":"Environment variable MONGODB_CONFIG_OVERRIDE_NOFORK == 1, overriding \"processManagement.fork\" to false"}

      TASK [Check mongod version.] ***********************************************************************
      changed: [127.0.0.1]

      TASK [Print mongod version.] ***********************************************************************
      ok: [127.0.0.1] =>
      msg: mongod_version.stdout

      TASK [Set bindIP to 0.0.0.0 in mongod.conf] ********************************************************
      changed: [127.0.0.1]

      TASK [Verify MongoDB Enterprise Edition installed successfully.] ***********************************
      changed: [127.0.0.1]

      TASK [Congratulations!] ****************************************************************************
      ok: [127.0.0.1] =>
      msg: MongoDB installation complete.

      PLAY RECAP *****************************************************************************************
      127.0.0.1                  : ok=13   changed=8    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

      [root@zdblab05 zmongodb]#
     
      ```

### MongoDB Uninstallation
#### Uninstall MongoDB
Run the ansible playbook to uninstall mongoDB. Use the following command:

``` bash
   ansible-playbook mongodbUnInstall.yml 
```

???- example "The following example shows the output of succesful MongoDB uninstalltion [click to expand me]"

      ```
      [root@zdblab05 zmongodb]# ansible-playbook mongodbUnInstall.yml

      PLAY [UnInstall MongoDB on a Linux Guest.] *********************************************************

      TASK [Gathering Facts] *****************************************************************************
      ok: [127.0.0.1]

      TASK [Gather info about installed  services.] ******************************************************
      ok: [127.0.0.1]

      TASK [Stop mongod service.] ************************************************************************
      changed: [127.0.0.1]

      TASK [Uninstall MongoDB.] **************************************************************************
      changed: [127.0.0.1]

      TASK [Remove data and log directories] *************************************************************
      ok: [127.0.0.1] => (item=/var/log/mongodb/mongod.log)
      changed: [127.0.0.1] => (item=/var/lib/mongodb)

      TASK [Done.] ***************************************************************************************
      ok: [127.0.0.1] =>
      msg: MongoDB has been uninstalled successfully.

      PLAY RECAP *****************************************************************************************
      127.0.0.1                  : ok=6    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

      [root@zdblab05 zmongodb]#
      ```
 
#### Install MongoDB 
In this step we will run the ansible playbook to install MongoDB back. Use the following command:

``` bash
   ansible-playbook mongodb8Install.yml 
```

???- example "The following example shows the output of succesful MongoDB installtion [click to expand me]"

      ```
      [root@zdblab05 zmongodb]# ansible-playbook mongodbInstall.yml

      PLAY [Install MongoDB on a Linux Guest.] ***********************************************************

      TASK [Gathering Facts] *****************************************************************************
      ok: [127.0.0.1]

      TASK [Create repo file for mongodb-enterprise] *****************************************************
      ok: [127.0.0.1]

      TASK [Install  mongodb-enterprise.] ****************************************************************
      changed: [127.0.0.1] => (item={'pkg': 'mongodb-enterprise', 'when': True})
      ok: [127.0.0.1] => (item={'pkg': 'libselinux-utils', 'when': "db_path != '/var/lib/mongodb' or log_file != '/var/log/mongodb/mongod.log'"})
      ok: [127.0.0.1] => (item={'pkg': 'policycoreutils-python-utils', 'when': "db_path != '/var/lib/mongodb' or log_file != '/var/log/mongodb/mongod.log'"})

      TASK [Set SELinux to Permissive mode.] *************************************************************
      skipping: [127.0.0.1]

      TASK [Disable SELinux permanently in configuration.] ***********************************************
      skipping: [127.0.0.1]

      TASK [Ensure db and log files exist and are owned by mongod user.] *********************************
      changed: [127.0.0.1] => (item={'path': '/var/lib/mongodb', 'state': 'directory', 'recurse': True})
      changed: [127.0.0.1] => (item={'path': '/var/log/mongodb/mongod.log', 'state': 'touch', 'recurse': False})

      TASK [Change db and/or log file paths.] ************************************************************
      changed: [127.0.0.1] => (item={'key': 'dbPath', 'value': '/var/lib/mongodb', 'when': "db_path != '/var/lib/mongodb'"})
      ok: [127.0.0.1] => (item={'key': 'path', 'value': '/var/log/mongodb/mongod.log', 'when': "log_file != '/var/log/mongodb/mongod.log'"})

      TASK [Start mongod service.] ***********************************************************************
      changed: [127.0.0.1]

      TASK [Check mongod status.] ************************************************************************
      changed: [127.0.0.1]

      TASK [Print mongod status.] ************************************************************************
      ok: [127.0.0.1] =>
      msg: |-
      ● mongod.service - MongoDB Database Server
       Loaded: loaded (/usr/lib/systemd/system/mongod.service; enabled; vendor preset: disabled)
       Active: active (running) since Mon 2025-03-10 21:51:38 UTC; 288ms ago
         Docs: https://docs.mongodb.org/manual
      Main PID: 490438 (mongod)
       Memory: 70.3M
       CGroup: /system.slice/mongod.service
               └─490438 /usr/bin/mongod -f /etc/mongod.conf

      Mar 10 21:51:38 zdblab05 systemd[1]: Started MongoDB Database Server.
      Mar 10 21:51:38 zdblab05 mongod[490438]: {"t":{"$date":"2025-03-10T21:51:38.431Z"},"s":"I",  "c":"CONTROL",  "id":7484500, "ctx":"main","msg":"Environment variable MONGODB_CONFIG_OVERRIDE_NOFORK == 1, overriding \"processManagement.fork\" to false"}

      TASK [Check mongod version.] ***********************************************************************
      changed: [127.0.0.1]

      TASK [Print mongod version.] ***********************************************************************
      ok: [127.0.0.1] =>
      msg: mongod_version.stdout

      TASK [Set bindIP to 0.0.0.0 in mongod.conf] ********************************************************
      changed: [127.0.0.1]

      TASK [Verify MongoDB Enterprise Edition installed successfully.] ***********************************
      changed: [127.0.0.1]

      TASK [Congratulations!] ****************************************************************************
      ok: [127.0.0.1] =>
      msg: MongoDB installation complete.

      PLAY RECAP *****************************************************************************************
      127.0.0.1                  : ok=13   changed=8    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

      [root@zdblab05 zmongodb]#
     
      ```
## Summary
 
In this lab we familiarized with basic Linux commands.      
