Ansiblize Systems
=========

This role is meant to setup and create an Ansible user with a username, password, SSH key, and to add the user to the SUDOERS file with password-less sudo access.

Requirements
------------

This role assumes that you are operating on an EL-based (RPM based) Linux distribution utilizing SystemD.

Role Variables
--------------

**ansible_user_name** - This variable is defined by default in the **defaults/main.yml** and is a required variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **username** to be created on the system and added to the **SUDOERS** file for password-less sudo capability.

**ansible_user_password** - This variable is defined by default in the **defaults/main.yml** and is an optional variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **password** to be created on the system for the given  **username**. If this variable is not defined a password will not be created for the user account.


**ssh_key_file_data** - This variable contains the value of the SSH public key of the specified user. This will be used to populate the authorized keys on the remote managed nodes for the user specified with the **ansible_user_name** variable. When provided, this will create the authorized key for the given user and ignore the task which will copy the current (local) user's SSH public key to the managed host.

**ssh_key_answer** - This variable is used when you want to copy the SSH public key of the current user. It leverages a **lookup** to grab the public SSH key of the current user and copy it to the managed host's authorized keys. It is IMPORTANT to note that if the **ssh_key_file_data** SSH key value is provided and defined for that variable, a **yes** for this variable will still ignore the task.

**ssh_root_allowed** - This is one of two optional variables controlling the SSHD service. This variable must be defined as either a **"yes"** or a **"no"** with the quotes and controls whether or not root is permitted to login to an SSH session.

**ssh_passwords_allowed** - This is one of two optional variables controlling the SSHD service. This variable must be defined as either a **"yes"** or a **"no"** with the quotes and controls whether or not a password is permitted to login to an SSH session or only SSH keys are allowed.


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
