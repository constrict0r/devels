Description
------------------------------------------------------------------------------

Ansible role to apply developer configuration.

This is capable of:

- Upgrade the system.

- Add `apt <https://wiki.debian.org/Apt>`_ repository sources.

- Update the apt cache.

- Uninstall apt packages.

- Install apt packages.

- Install `yarn <https://yarnpkg.com>`_ packages.

- Install `pip <https://pypi.org/project/pip/>`_ packages.

- Apply system-wide configuration using git.

- Stop services and disable them.

- Enable services and restart them.

- Create users.

- Add users to groups.

- Apply user-wide configuration using git.

- Run custom user tasks.

By default this role applies the following configuration:

- Installs the base software:

 .. include:: parts/packages/base.inc

- Installs the base developer software:

 .. include:: parts/packages/dev_base.inc

- Installs the python developer software:

 .. include:: parts/packages/dev_python.inc

- Installs the microcontroller developer software:

 .. include:: parts/packages/dev_micro.inc

- Configures the base software:

 .. include:: parts/configured/base.inc

- Configures the base developer software:

 .. include:: parts/configured/dev_base.inc

- Configures the python developer software:

 .. include:: parts/configured/dev_python.inc

- Configures the microcontroller developer software:

 .. include:: parts/configured/dev_micro.inc

- Creates the following home directory layout:

 .. code-block:: bash

  home/
  ├── .emacs.d
  │   ├── config
  │   │   ├── base.el
  │   │   ├── org.el
  |   │   └── python.el
  │   ├── init.el
  │   └── themes
  │       └── wintermute-theme.el
  └── .vimrc

- Modifies the following files:

 .. code-block:: bash

  home/
  ├── .bashrc
  └── .profile
