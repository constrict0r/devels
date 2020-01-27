
Description
***********

Ansible role to apply developer configuration.

This is capable of:

* Upgrade the system.

* Add `apt <https://wiki.debian.org/Apt>`_ repository sources.

* Updated the apt cache.

* Uninstall apt packages.

* Install apt packages.

* Install `npm <http://npmjs.org/>`_ packages.

* Install `pip <https://pypi.org/project/pip/>`_ packages.

* Apply system-wide configuration using git.

* Stop services and disable them.

* Enable services and restart them.

* Create users.

* Add users to groups.

* Apply user-wide configuration using git.

* Run custom user tasks.

By default this role applies the following configuration:

* Installs the base software:

..

   * apt-transport-https

   * bzip2

   * ca-certificates

   * curl

   * sudo

   * unrar-free

   * unzip

   * vim

   * wget

   * xz-utils

* Installs the base developer software:

..

   * bats

   * emacs

   * git

   * libtext-csv-perl

   * make

   * meld

   * retext

   * ssh-askpass

   * tree

* Installs the python developer software:

..

   * Via apt:

   ..

      * direnv

      * python3

      * python3-pip

      * python3-pytest

      * python3-venv

      * python3-virtualenv

      * tox

   * Via pip:

   ..

      * ansible-lint

      * autopep8

      * flake8

      * jedi

      * poetry

      * sphinx

      * sphinx_rtd_theme

      * rope

      * yapf

* Configures the base software:

..

   * vim

   ..

      * Creates a *.vimrc* configuration file on each user home
         directory.

      * Enable syntax highlight.

      * Set two spaces instead of tabs.

* Configures the base developer software:

..

   * emacs

   ..

      * Creates a *.emacs.d* configuration folder on each user home
         directory.

      * Enable line numbers.

      * Set themes folder.

      * Set wintermute theme.

      * Use spaces instead of tabs.

* Configures the python developer software:

..

   * direnv

   ..

      * Enable *direnv* command on *~/.bashrc* file.

   * emacs

   ..

      * Set `elpy <https://is.gd/tPU9gM>`_ plugin.

      * Set `tox.el <https://is.gd/hUqDMw>`_ plugin.

      * Set keybindings:

      ..

         * C-c C-c: Evaluates the current script.

         * C-RET (Enter): Evaluates the curren statement (current
            line plus the
               following nested line).

         * C-c C-z: Switches between your script and the interactive
            shell.

         * C-c C-d: Displays documentation for the thing under cursor
            (function or module). The documentation will pop in a
            different buffer, can be closed with *q*.

         * C-c C-t: Run pytest tests.

         * M-x tox-current-test: Run tox tests for current test.

         * M-x tox-current-class: Run tox tests for current class.

         * M-x pdb: Run PDB on a new window.

         * C-x: Set breakpoint on current line.

   * `poetry <https://poetry.eustace.io/>`_

   ..

      * Add poetry path to the *~/.profile* file to maintain
         dependecies aisolated.

   * `python3-virtualenv <https://virtualenv.pypa.io/en/latest/>`_

   ..

      * Enable elpy virtual enviroments on the *~/.bashrc* file.

* Creates the following home directory layout:

..

   ::

      home/
      ├── .emacs.d
      │   ├── base.el
      │   ├── init.el
      │   ├── python.el
      │   └── themes
      │       └── wintermute-theme.el
      └── .vimrc

* Modifies the following files:

..

   ::

      home/
      ├── .bashrc
      └── .profile
