ansible-common
==============

Ansible role for common configuration tasks on EL7 servers.

Requirements
------------

Currently, the role only supports `CentOS`_ and
`Red Hat Enterprise Linux (RHEL)`_ EL7 distribution flavors.

If you need support for other flavors, feel free to `submit a pull request`_.

.. _CentOS: https://www.centos.org/
.. _Red Hat Enterprise Linux (RHEL):
  https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux
.. _submit a pull request:
  https://github.com/dblenkus/ansible-common/pull/new/master

Role Variables
--------------

``remote_user`` variable is automatically set with running ``whoami``
command as user who connects to the server.

+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default              |
+====================================+==========+===========================================+===========+===================================+
| ``common_include_security``        |  boolean | Specify if part of the role in charge of  |     no    |             ``true``              |
|                                    |          | security is played or not.                |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_include_guest_additions`` |  boolean | Specify if part of the role in charge of  |     no    |             ``false``             |
|                                    |          | installing the VirtualBox's guest         |           |                                   |
|                                    |          | additions is played or not.               |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_hostname``                |  string  | Hostname of the server.                   |     no    | ``"{{ inventory_hostname }}"``    |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_rhel_repos_for_epel``     |   list   | List of repository ids that need to be    |     no    | ``- rhel-7-server-optional-rpms`` |
|                                    |          | enabled on RHEL machines for the `EPEL    |           |                                   |
|                                    |          | repository`_.                             |           | ``- rhel-7-server-extras-rpms``   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_python3_enabled``         |  boolean | Install Python 3 if ``true``.             |     no    |             ``false``             |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_selinux_permisive``       |  boolean | Set SELinux to permisive mode if ``true``.|     no    |             ``false``             |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_ssh_allowed_ips``         |   list   | List of ip addresses from which firewall  |     no    |              ``[]``               |
|                                    |          | will allow ssh connection.                |           |                                   |
|                                    |          |                                           |           |                                   |
|                                    |          | .. WARNING::                              |           |                                   |
|                                    |          |    If list is empty, all ssh connections  |           |                                   |
|                                    |          |    will be allowed.                       |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_ssh_authorized_keys``     |   list   | List of public ssh keys which will be     |     no    |              ``[]``               |
|                                    |          | added to ``remote_user``'s                |           |                                   |
|                                    |          | ``authorized_keys file``.                 |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``vaulted_common_root_password``   |  string  | ``root``'s password. It must be hashed    |     no    |              ``""``               |
|                                    |          | and stored in Ansible Vault for security  |           |                                   |
|                                    |          | reasons. See `Ansible documentation`_ for |           |                                   |
|                                    |          | more details.                             |           |                                   |
|                                    |          |                                           |           |                                   |
|                                    |          | .. WARNING::                              |           |                                   |
|                                    |          |    Password will be disabled if this      |           |                                   |
|                                    |          |    setting is left blank.                 |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_root_ps1``                |  string  | Value of ``root``'s ``PS1`` bash variable |     no    |                                   |
|                                    |          | if defined.                               |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``vaulted_common_user_password``   |  string  | ``remote_user``'s password. It must be    |     no    |                                   |
|                                    |          | hashed and stored in Ansible Vault for    |           |                                   |
|                                    |          | security reasons. See `Ansible            |           |                                   |
|                                    |          | documentation`_ for more details.         |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_user_ps1``                |  string  | Value of ``remote_user``'s PS1 bash       |     no    |                                   |
|                                    |          | variable if defined.                      |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+
| ``common_virtualbox_dist_dir``     |  string  | Path where VirtualBox guest additions     |     no    |         ``/opt/virtualbox``       |
|                                    |          | will be downloaded and extracted.         |           |                                   |
+------------------------------------+----------+-------------------------------------------+-----------+-----------------------------------+

.. _Ansible documentation: http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module
.. _EPEL repository: https://fedoraproject.org/wiki/EPEL

Dependencies
------------

No dependencies.

Example Playbook
----------------

To use this role add this to your playbook:

.. code-block:: yaml

    - hosts: servers
      roles:
         - { role: domenblenkus.common }

License
-------

Licensed under the GPLv3 License. See the COPYING file for details.

Author Information
------------------

| Domen Blenkuš
| Tadej Janež
