ansible-leapp
=============

This Ansible role attempts to perform an automated in-place upgrade of EL based
systems, primarily Red Hat Enterprise Linux.

It performs the following high level tasks:

* Validating prerequisites and requirements
* Preparing a system for the upgrade
* Generate leapp preupgrade report
* Remediate common upgrade issues (disabled by default)
* Performing the upgrade (disabled by default)
* Verifying the post-upgrade state (disabled by default)

By default, this role will not perform the actual upgrade.  It is intended to
prepare the system and generate a preupgrade report that should be reviewed.
If you're feeling lucky, you can also have it attempt to perform the upgrade.

TODO
----

* Implement post-upgrade verification (tasks/verify.yml)

References
----------

I used the following docs for reference:

* [https://developers.redhat.com/products/rhel/download](https://developers.redhat.com/products/rhel/download)
* [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/upgrading_from_rhel_7_to_rhel_8/index](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/upgrading_from_rhel_7_to_rhel_8/index)
* [https://www.redhat.com/en/blog/upgrading-rhel-7-rhel-8-leapp-and-boom](https://www.redhat.com/en/blog/upgrading-rhel-7-rhel-8-leapp-and-boom)
* [https://access.redhat.com/articles/4263361](https://access.redhat.com/articles/4263361)
* [https://access.redhat.com/articles/3664871](https://access.redhat.com/articles/3664871)

Role Variables
--------------

Variables that modify the behavior of this role are declared in `defaults/main.yml`

```
# Provide a list of repository IDs that exist in /etc/yum.repos.d
# Default []
leapp_custom_repositories: []

# specify a grub device, generally not required for most installations
leapp_grub_device: '/boot'

# Skip Red Hat Subscription Manager? Default no
leapp_skip_rhsm: no

# Skip the validation pre-flight checks? Default no
leapp_skip_validate: no

# Skip the prepare tasks? Default no
leapp_skip_prepare: no

# Skip cockpit installation? Default no
leapp_skip_prepare_cockpit_install: no

# Skip package installation?  Default no
leapp_skip_prepare_package_install: no

# Skip actual package updates?  Default yes
leapp_skip_prepare_update: yes

# Skip reboot after changes to package updates?  Default no
leapp_skip_prepare_update_reboot: no

# Skip the leapp preupgrade? Default yes
leapp_skip_preupgrade: yes

# Skip removing previous reports?  Defaults no
leapp_skip_preupgrade_cleanup: no

# Skip remediate of common issues?  Defaults yes
leapp_skip_remediate: yes

# Skip the actual leapp upgrade? Default yes
leapp_skip_upgrade: yes

# How long to wait (in seconds) for reboot after upgrade? Default 1200
leapp_reboot_timeout: 1200
```

Dependencies
------------

There are no dependencies to use this role, however, this role assumes you have
implemented a standard operating environment that provides:

* Red Hat Enterprise Linux 7
* System Entitled with RHSM or Satellite
* Repositories configured and enabled for latest updates, specifically for
  `rhel-7-server-rpms` and `rhel-7-server-extras-rpms`

Additionally, you must also download the additional required data files (RPM
package changes and RPM repository mapping) attached to the
[Knowledgebase Article](https://access.redhat.com/articles/3664871) and place
it in the 'files' directory in the same directory as the playbook including
this role.

Example Playbook
----------------

The following is a simple playbook that will perform the default behaviors up to
performing the actual upgrade:

```
---

- name: Perform an in-place upgrade of a EL System
  hosts: all
  become: yes

  vars:
    # Provide a list of repository IDs that exist in /etc/yum.repos.d
    # Default []
    leapp_custom_repositories: []

    # Skip Red Hat Subscription Manager? Default no
    leapp_skip_rhsm: no

    # Skip the validation pre-flight checks? Default no
    leapp_skip_validate: no

    # Skip the prepare tasks? Default no
    leapp_skip_prepare: no

    # Skip cockpit installation? Default no
    leapp_skip_prepare_cockpit_install: no

    # Skip package installation?  Default no
    leapp_skip_prepare_package_install: no

    # Skip actual package updates?  Default yes
    leapp_skip_prepare_update: yes

    # Skip the leapp preupgrade? Default no
    leapp_skip_preupgrade: no

    # Skip removing previous reports?  Defaults no
    leapp_skip_preupgrade_cleanup: no

    # Skip the actual leapp upgrade? Default yes
    leapp_skip_upgrade: yes

    # How long to wait (in seconds) for reboot after upgrade? Default 1200
    leapp_reboot_timeout: 1200

  roles:
    - mrjoshuap.leapp
```

License
-------

GPL-2.0-or-later

Author Information
------------------

Joshua Preston is a solution architect with Red Hat, specializing in Platform
and Management technologies.
