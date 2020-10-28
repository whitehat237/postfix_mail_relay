Role Name
=========

An Ansible Role to install and configure postfix, and configure postfix to use 
Google's SMTP service to relay mail for root, to a specified user.
A self signed cert is created, and postfix is configured to use that 
certificate for SASL.

Requirements
------------
An Ansible vault to store username and password located in files/

I.E.
$ ansible-vault create files/postfix_mail_relay_vault.yml

Set a password for the vault.

The vault should contain the following variables:

postfix_mail_relay_vault_username: someuser@gmail.com
postfix_mail_relay_vault_password: google-application-pa$$word1

Required variables must set in vars/main.yml


Role Variables
--------------
target				- The remote target node.
postfix_mail_relay  		- The hostname of the mail relay to be used.  I.E. smtp.gmail.com
postfix_mail_relay_port 	- The port specification.  I.E. 587
country				- The C value used during certificate creation
state				- The ST value used during certificate creation
local				- The L value used during certificate creation
org				- The O value used during certificate creation
ou				- The OU value used during certificate creation


Dependencies
------------


Example Playbook
----------------

--

- name: playbook to run postfix_mail_relay role
  become: yes
  become_flags: -H -S
  hosts: "{{ target }}"
  gather_facts: yes

  vars_files:
    - files/postfix_mail_relay_vault.yml
    - vars/main.yml

  roles:
    - postfix_mail_relay



License
-------
GPL-2.0 and later

Author Information
------------------

whitehat237@gmail.com
