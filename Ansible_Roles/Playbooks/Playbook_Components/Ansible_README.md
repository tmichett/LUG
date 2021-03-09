Ansiblize Systems
=========

This role is meant to setup and create an Ansible user with a username, password, SSH key, and to add the user to the SUDOERS file with password-less sudo access.

Requirements
------------

This role assumes that you are operating on an EL-based Linux distribution utilizing SystemD.

Role Variables
--------------

**pkg_name** - This variable is the name of the package or a list of package names that can be installed on the system. This is the "ONLY" required variable to be supplied.

**pkg_state** - This variable is a default variable and set to "latest". The allowed values for this variable are "latest" and "present" to install the package(s) or "absent" to ensure that the package has been removed.

Dependencies
------------

There are no dependencies for this playbook, but there is another related role published to work with Linux services.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:



    ---
    - name: Install Software Packages
      hosts: serverc
      vars:
        pkg_name:
          - vim
          - tree
          - httpd
      roles:
        - tmichett.deploy_packages



License
-------

BSD

Author Information
------------------

Travis Michette
tmichett@redhat.com
