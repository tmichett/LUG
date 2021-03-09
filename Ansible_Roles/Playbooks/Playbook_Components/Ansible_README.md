Ansiblize Systems
=========

This role is meant to setup and create an Ansible user with a username, password, SSH key, and to add the user to the SUDOERS file with password-less sudo access.

Requirements
------------

This role assumes that you are operating on an EL-based (RPM based) Linux distribution utilizing SystemD.

Role Variables
--------------

**ansible_user_name** - This variable is defined by default in the **defaults/main.yml** and is a required variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **username** to be created on the system and added to the **SUDOERS** file for password-less sudo capability.

**ansible_user_password** - This variable is defined by default in the **defaults/main.yml** and is an optional variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **password** to be created on the system for the given  **username**.


**ssh_key_file_data** - This variable is a default variable and set to "latest". The allowed values for this variable are "latest" and "present" to install the package(s) or "absent" to ensure that the package has been removed.

**ssh_key_answer** - This variable is a default variable and set to "latest". The allowed values for this variable are "latest" and "present" to install the package(s) or "absent" to ensure that the package has been removed.

**ssh_root_allowed** - This variable is a default variable and set to "latest". The allowed values for this variable are "latest" and "present" to install the package(s) or "absent" to ensure that the package has been removed.

**ssh_passwords_allowed** - This variable is a default variable and set to "latest". The allowed values for this variable are "latest" and "present" to install the package(s) or "absent" to ensure that the package has been removed.


Dependencies
------------

There are no dependencies for this playbook, but there is another related role published to work with Linux services.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:



    ---
    - name: Ansiblize my Systems
      hosts: servera
      vars:
        pkg_name:
          - vim
          - tree
          - httpd
      roles:
        - tmichett.ansiblize



License
-------

BSD

Author Information
------------------

Travis Michette
tmichett@redhat.com
