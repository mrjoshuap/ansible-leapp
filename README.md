Leapp
=====

This role attempts to perform an automated in-place upgrade of EL based systems, primarily Red Hat Enterprise Linux.

References
----------

I used the following docs for reference:

* https://developers.redhat.com/products/rhel/download
* https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/upgrading_from_rhel_7_to_rhel_8/index
* https://www.redhat.com/en/blog/upgrading-rhel-7-rhel-8-leapp-and-boom
* https://access.redhat.com/articles/4263361

Role Variables
--------------

Variables that modify the behavior of this role are declared in `defaults/main.yml`

```
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

# Skip actual package updates?  Default no
leapp_skip_prepare_update: no

# Skip the leapp preupgrade? Default no
leapp_skip_preupgrade: yes

# Skip removing previous reports?  Defaults no
leapp_skip_preupgrade_cleanup: no

# Skip the actual leapp upgrade? Default yes
leapp_skip_upgrade: yes

# How long to wait (in seconds) for reboot after upgrade? Default 1200
leapp_upgrade_reboot_timeout: 1200
```

Dependencies
------------

There are no dependencies to use this role, however, this role assumes you have implemented a standard operating environment that provides:

* Red Hat Enterprise Linux 7
* System Entitled with RHSM or Satellite
* Repositories configured and enabled for latest updates, specifically for `rhel-7-server-rpms` and `rhel-7-server-extras-rpms`

Example Playbook
----------------

The following is a simple playbook that will perform everything up to performing the actual upgrade:

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

    # Skip actual package updates?  Default no
    leapp_skip_prepare_update: no

    # Skip the leapp preupgrade? Default no
    leapp_skip_preupgrade: yes

    # Skip removing previous reports?  Defaults no
    leapp_skip_preupgrade_cleanup: no

    # Skip the actual leapp upgrade? Default yes
    leapp_skip_upgrade: yes

    # How long to wait (in seconds) for reboot after upgrade? Default 1200
    leapp_upgrade_reboot_timeout: 1200

  roles:
    - mrjoshuap.leapp
```

License
-------

GPL-2.0-or-later

Author Information
------------------

Joshua Preston is a solution architect with Red Hat, specializing in Platform and Management technologies.
