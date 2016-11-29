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

+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default               |
+====================================+==========+===========================================+===========+====================================+
| ``common_include_security``        |  boolean | Specify if part of the role in charge of  |     no    |                true                |
|                                    |          | security is played or not.                |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_include_guest_additions`` |  boolean | Specify if part of the role in charge of  |     no    |                false               |
|                                    |          | installing the VirtualBox's guest         |           |                                    |
|                                    |          | additions is played or not.               |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_include_postfix``         |  boolean | Specify if part of the role in charge of  |     no    |                true                |
|                                    |          | installing the Postfix is played or not.  |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_selinux_permisive``       |  boolean | Set SELinux to permisive mode if ``true``.|     no    |                false               |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ssh_allowed_ips``         |   list   | List of ip addresses from which firewall  |     no    |                 []                 |
|                                    |          | will allow ssh connection.                |           |                                    |
|                                    |          |                                           |           |                                    |
|                                    |          | .. WARNING::                              |           |                                    |
|                                    |          |    If list is empty, all ssh connections  |           |                                    |
|                                    |          |    will be allowed.                       |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ssh_authorized_keys``     |   list   | List of public ssh keys which will be     |     no    |                 []                 |
|                                    |          | added to ``remote_user``'s                |           |                                    |
|                                    |          | ``authorized_keys file``.                 |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_common_root_password``   |  string  | ``root``'s password. It must be hashed    |     no    |                 ""                 |
|                                    |          | and stored to ansible-vault for security  |           |                                    |
|                                    |          | reasons. See `this`__ link for more       |           |                                    |
|                                    |          | details.                                  |           |                                    |
|                                    |          |                                           |           |                                    |
|                                    |          | .. WARNING::                              |           |                                    |
|                                    |          |    Password will be disabled if this      |           |                                    |
|                                    |          |    setting is left blank.                 |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_root_ps1``                |  string  | Value of ``root``'s ``PS1`` bash variable |     no    |                                    |
|                                    |          | if defined.                               |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_common_user_password``   |  string  | ``remote_user``'s password. It must be    |     no    |                                    |
|                                    |          | hashed and stored to ansible-vault for    |           |                                    |
|                                    |          | security reasons. See `this`__ link for   |           |                                    |
|                                    |          | more details.                             |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_user_ps1``                |  string  | Value of ``remote_user``'s PS1 bash       |     no    |                                    |
|                                    |          | variable if defined.                      |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_virtualbox_dist_dir``     |  string  | Path where VirtualBox guest additions     |     no    |         ``/opt/virtualbox``        |
|                                    |          | will be downloaded and extracted.         |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ses_host``                |  string  | Hostname of AWS SES server.               |     no    | email-smtp.eu-west-1.amazonaws.com |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ses_port``                |  integer | Port of AWS SES server.                   |     no    |                 25                 |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ses_username``            |  string  | Username for authenticating with AWS SES  |    yes    |                                    |
|                                    |          | server.                                   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_common_ses_password``    |  string  | Password for authenticating with AWS SES  |    yes    |                                    |
|                                    |          | server.                                   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``common_ses_from_email``          |  string  | Email address which will be used as       |    yes    |                                    |
|                                    |          | `From` address.                           |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+

.. __: http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module

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
