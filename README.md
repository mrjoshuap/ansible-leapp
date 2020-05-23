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

Requirements
------------

This role assumes you have implemented a standard operating environment that provides:

* Red Hat Enterprise Linux 7
* System Entitled with RHSM or Satellite
* Repositories configured and enabled for latest updates, specifically for `rhel-7-server-rpms` and `rhel-7-server-extras-rpms`

Role Variables
--------------

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

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

Joshua Preston is a solution architect with Red Hat, specializing in Platform and Management technologies.
