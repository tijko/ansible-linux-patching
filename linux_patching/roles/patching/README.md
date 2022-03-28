patching
=========

This role to updates the linux system ( Redhat or Centos ) as follows:  
1- Prechecks like Repository checks, and gather all your mandatory checks information(mount,ip details,routing,services,etc).  
2- if repository is success, patch the server.  
3- if patch the server reboot.  
4- wait for  server booting, once back and validate your server with your precheck data.  


There are 2 Patching_type you can use:  
  - NOREBOOT
  - KERNEL (FULL )

Role Variables
--------------
The variables that can be passed to this role are as follows:  
```
supported_distros:  
  - Redhat
  - CentOS
```
local_dir is a directory where to store the logs during the playbooks is running. Default: /tmp/ansible/sys-patching:  
local_dir: "/tmp/ansible/sys-patching"  

Patching_type: KERNEL --> Full patch with reboot , NOREBOOT . Default: KERNEL:  
Patching_type:  KERNEL  

Requirements
------------
These playbooks were designed to be used in Linux system  (RHEL and centos for now ). You need to have a valid yum repository on each managed node.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too :)  
```
---  
- name: Patching the linux system using patching roles  
  hosts: all  
  become: true  
  vars:  
    Patching_type: "KERNEL"  
  roles:  
    - patching  
```

Expected result  
---------------  

```
        "UPDATE SUMMARY", 
        [
            "", 
            "\"HOSTNAME: node1 version before the update:\"", 
            "\"      distribution: CentOS \"", 
            "\"      distribution_major_version: 7\"", 
            "\"      distribution_release: Core\"", 
            "\"      distribution_version: 7.3\"", 
            "", 
            "HOSTNAME: node1 | getty@tty1.service : OK ", 
            "HOSTNAME: node1 | firewalld.service : OK ", 
            "HOSTNAME: node1 | network : OK ", 
            "HOSTNAME: node1 | postfix.service : OK ", 
            "HOSTNAME: node1 | rsyslog.service : OK ", 
	     .
	     .
 	     .
	     omitted

            "HOSTNAME: node1 | /dev/sdc1                      1014M  156M  859M  16% /boot : MOUNTED ", 
            "HOSTNAME: node1 | /dev/mapper/test_vg1-test_lvm1  197M   11M  187M   6% /test/lvm1 : ****NOT MOUNTED**** ", 
            "HOSTNAME: node1 | /dev/mapper/test_vg2-test_lvm3  197M   11M  187M   6% /test/lvm3 : MOUNTED ", 
	    "HOSTNAME: node1 | yum update succeeded."
            "HOSTNAME: node1 | interface enp0s3 : OK  ", 
            "HOSTNAME: node1 | interface enp0s3 : 192.168.0.16 : OK  ",	
	    "HOSTNAME: node1 | ***SELinux status changed***",
	    "# BEGIN ANSIBLE MANAGED BLOCK", 
            "\"HOSTNAME: node1 version After the update:\"", 
            "\"      distribution: CentOS \"", 
            "\"      distribution_major_version: 7\"", 
            "\"      distribution_release: Core\"", 
            "\"      distribution_version: 7.8\"", 
            "# END ANSIBLE MANAGED BLOCK",
```
  
License
-------

BSD

Author Information
------------------

For Help Contact me : **Ahmed Hagag**

     ahmed.thagag@gmail.com
