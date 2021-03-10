Ansiblize Systems
=========

This role is meant to setup and create an Ansible user with a username, password, SSH key, and to add the user to the SUDOERS file with password-less sudo access.

Requirements
------------

This role assumes that you are operating on an EL-based (RPM based) Linux distribution utilizing SystemD.

Role Variables
--------------

**ansible_user_name** - This variable is defined by default in the **defaults/main.yml** and is a required variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **username** to be created on the system and added to the **SUDOERS** file for password-less sudo capability.

**ansible_user_password** - This is an optional variable for the playbook. It is suggested to use this variable in the playbook designed to use the role. This variable defines the **password** to be created on the system for the given  **username**. If this variable is not defined a password will not be created for the user account.


**ssh_key_file_data** - This variable contains the value of the SSH public key of the specified user. This will be used to populate the authorized keys on the remote managed nodes for the user specified with the **ansible_user_name** variable. When provided, this will create the authorized key for the given user and ignore the task which will copy the current (local) user's SSH public key to the managed host.

**ssh_key_answer** - This variable is used when you want to copy the SSH public key of the current user. It leverages a **lookup** to grab the public SSH key of the current user and copy it to the managed host's authorized keys. It is IMPORTANT to note that if the **ssh_key_file_data** SSH key value is provided and defined for that variable, a **yes** for this variable will still ignore the task.  This variable is defined by default in the **defaults/main.yml** and is set to **no**.

**ssh_root_allowed** - This is one of two optional variables controlling the SSHD service. This variable must be defined as either a **"yes"** or a **"no"** with the quotes and controls whether or not root is permitted to login to an SSH session.

**ssh_passwords_allowed** - This is one of two optional variables controlling the SSHD service. This variable must be defined as either a **"yes"** or a **"no"** with the quotes and controls whether or not a password is permitted to login to an SSH session or only SSH keys are allowed.


Dependencies
------------

There are no dependencies for this playbook.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:


**Simple Playbook with a Username and Password**

    ---
    - name: Ansiblize Managed Hosts - Demo Test
      hosts: all
      vars:
        ansible_user_name: travis
        ansible_user_password: redhat
      roles:
        - tmichett.demo_role


**Simple Playbook with a Username and Password (but the playbook prompts for the password)**

    ---
    - name: Ansiblize Managed Hosts - Demo Test

      hosts: all

      vars:
        ansible_user_name: travis

      vars_prompt:
        - name: ansible_user_password
          prompt: What password would you like to define for the Ansible user?

      roles:
        - tmichett.demo_role


**Simple Playbook with a Username and Password and SSH Key Provided**

    ---
    - name: Ansiblize Managed Hosts - Demo Test

      hosts: all

      vars:
        ansible_user_name: travis
        ssh_key_file_data: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDSmPWK8JpLCWn2LhjoR1Rdvb6NUbQdhqQAoZ15+OWNjCEmVZV9pReuPmCmM1uiAz+NlExvjpF3uxPeKf7Z5GqoVO/YzP5KFqPSH6J0TpxilBc+5uSJnZoS+9oB+0jFVT5hpb99ZT85mLEsSoOLDlposy8SAunr8w5JhaaIuz7Is+GDPejuAtCEQmEcDJJl4IPnxt6X0YJ+NZQDt2mkWuSP2EIsl470LNu9OAUN19JfJe56PcjUoqedu+IXyjP16d+GldjaV1aomnTZKxLvmDTkCDO56H88bhQWX4XUvyystf/E1Bji72cWy57kwf93Jblh2DE6Vu8d6COkNHckQCHl ansible-user@workstation.lab.example.com

      vars_prompt:
        - name: ansible_user_password
          prompt: What password would you like to define for the Ansible user?

      roles:
        - tmichett.demo_role

**Simple Playbook with a Username and Password and SSH Key Provided and Changing SSHD Services Daemon**

    ---
    - name: Ansiblize Managed Hosts - Demo Test
      hosts: all
      vars:
        ansible_user_name: travis
        ssh_key_file_data: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDSmPWK8JpLCWn2LhjoR1Rdvb6NUbQdhqQAoZ15+OWNjCEmVZV9pReuPmCmM1uiAz+NlExvjpF3uxPeKf7Z5GqoVO/YzP5KFqPSH6J0TpxilBc+5uSJnZoS+9oB+0jFVT5hpb99ZT85mLEsSoOLDlposy8SAunr8w5JhaaIuz7Is+GDPejuAtCEQmEcDJJl4IPnxt6X0YJ+NZQDt2mkWuSP2EIsl470LNu9OAUN19JfJe56PcjUoqedu+IXyjP16d+GldjaV1aomnTZKxLvmDTkCDO56H88bhQWX4XUvyystf/E1Bji72cWy57kwf93Jblh2DE6Vu8d6COkNHckQCHl ansible-user@workstation.lab.example.com

        ### These variables cause the role to reconfigure the SSHD Service/Daemon to allow/disallow root or password logins.

        ssh_root_allowed: "no" # Must have "yes" or "no" in quotes
        ssh_passwords_allowed: "no" # Must have "yes" or "no" in quotes

        vars_prompt:
          - name: ansible_user_password
            prompt: What password would you like to define for the Ansible user?

        roles:
          - tmichett.demo_role


License
-------

BSD

Author Information
------------------

Travis Michette
tmichett@redhat.com
