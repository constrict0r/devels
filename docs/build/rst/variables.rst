
Variables
*********

The following variables are supported:


expand
======

Boolean value indicating if load items from file paths or URLs or just
treat files and URLs as plain text.

If set to *true* this role will attempt to load items from the
especified paths and URLs.

If set to *false* each file path or URL found on packages will be
treated as plain text.

This variable is set to *false* by default.

::

   ansible localhost -m include_role -a name=constrict0r.devels \
       -e "expand=true configuration='/home/username/my-config.yml' titles='packages'"

If you wish to override the value of this variable, specify an
*item_path* and an *item_expand* attributes when passing the item, the
*item_path* attribute can be used with URLs too:

::

   ansible localhost -m include_role -a name=constrict0r.devels \
       -e "{expand: false,
           packages: [ \
               item_path: '/home/username/my-config.yml', \
               item_expand: false \
           ], titles: 'packages'}"

To prevent any unexpected behaviour, it is recommended to always
specify this variable when calling this role.


group
=====

List of groups to add all users into. Each non-empty username will be
added to the groups specified on this variable.

This list can be modified by passing an *groups* array when including
the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{group: [disk, sudo]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         group:
           - disk
           - sudo

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{group: [disk, sudo]}"


packages
========

List of packages to install via apt.

This list can be modified by passing a *packages* array when including
the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{packages: [gedit, rolldice]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         packages:
           - gedit
           - rolldice

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{packages: [gedit, rolldice]}"


packages_npm
============

List of packages to install via npm.

This list can be modified by passing a *packages_npm* array when
including the role on a playbook or via *–extra-vars* from a terminal.

If you want to install a specific package version, then specify *name*
and *version* attributes for the package.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{packages_npm: [node-red, {name: requests, version: 2.22.0}]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         packages_npm:
           - node-red
           - name: requests
             version: 2.22.0

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{packages_npm: [node-red, {name: requests, version: 2.22.0}]}"


packages_pip
============

List of packages to install via pip.

This list can be modified by passing a *packages_pip* array when
including the role on a playbook or via *–extra-vars* from a terminal.

If you want to install a specific package version, append the version
to the package name.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{packages_pip: ['bottle==0.12.17', 'whisper']}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         packages_pip:
           - bottle==0.12.17
           - whisper

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{packages_pip: ['bottle==0.12.17', 'whisper']}"


packages_purge
==============

List of packages to purge using apt.

This list can be modified by passing a *packages_purge* array when
including the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{packages_purge: [gedit, rolldice]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         packages_purge:
           - gedit
           - rolldice

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{packages_purge: [gedit, rolldice]}"


password
========

If an user do not specifies the *password* attribute, this password
will be setted for that user.

This password will only be setted for new users and do not affects
existent users.

This variable defaults to 1234.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{password: 4321}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         password: 4321

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "password=4321"


repositories
============

List of repositories to add to the apt sources.

This list can be modified by passing a *repositories* array when
including the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{repositories: [{ \
            name: multimedia, \
            repo: 'deb http://www.debian-multimedia.org sid main' \
        }]}}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         repositories:
           - name: multimedia
             repo: deb http://www.debian-multimedia.org sid main

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{repositories: [{ \
            name: multimedia, \
            repo: 'deb http://www.debian-multimedia.org sid main' \
        }]}}"


services
========

List of services to enable and start.

This list can be modified by passing a *services* array when including
the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{services: [mosquitto, nginx]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         services:
           - mosquitto
           - nginx

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{services: [mosquitto, nginx]}"


services_disable
================

List of services to stop and disable.

This list can be modified by passing a *services_disable* array when
including the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{services_disable: [mosquitto, nginx]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         services_disable:
           - mosquitto
           - nginx

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{services_disable: [mosquitto, nginx]}"


system_skeleton
===============

URL or list of URLs pointing to git skeleton repositories containing
layouts of directories and configuration files.

Each URL on system_skeleton will be checked to see if it points to a
valid git repository, and if it does, the git repository is cloned.

The contents of each cloned repository will then be copied to the root
of the filesystem as a simple method to apply system-wide
configuration.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{system_skeleton: [https://gitlab.com/huertico/server]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         system_skeleton:
           - https://gitlab.com/huertico/server
           - https://gitlab.com/huertico/client

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{system_skeleton: [https://gitlab.com/huertico/server]}"


upgrade
=======

Boolean variable that defines if a system full upgrade is performed or
not.

If set to *true* a full system upgrade is executed.

This variable is set to *true* by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "upgrade=false"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         upgrade: false

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "upgrade=false"


users
=====

List of users to be created. Each non-empty username listed on users
will be created.

This list can be modified by passing an *users* array when including
the role on a playbook or via *–extra-vars* from a terminal.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{users: [mary, jhon]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         users:
           - mary
           - jhon

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{users: [mary, jhon]}"


user_skeleton
=============

URL or list of URLs pointing to git skeleton repositories containing
layouts of directories and configuration files.

Each URL on system_skeleton will be checked to see if it points to a
valid git repository, and if it does, the git repository is cloned.

The contents of each cloned repository will then be copied to each
user home directory.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{user_skeleton: [https://gitlab.com/constrict0r/home]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         user_skeleton:
           - https://gitlab.com/constrict0r/home

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{user_skeleton: [https://gitlab.com/constrict0r/home]}"


user_tasks
==========

Absolute file path or URL to a *.yml* file containing ansible tasks to
execute.

Each file or URL on this variable will be checked to see if it exists
and if it does, the task is executed.

This variable is empty by default.

::

   # Including from terminal.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "{user_tasks: [https://is.gd/vVCfKI]}"

   # Including on a playbook.
   - hosts: servers
     roles:
       - role: constrict0r.devels
         user_tasks:
           - https://is.gd/vVCfKI

   # To a playbook from terminal.
   ansible-playbook -i tests/inventory tests/test-playbook.yml -K -e \
       "{user_tasks: [https://is.gd/vVCfKI]}"


configuration
=============

Absolute file path or URL to a *.yml* file that contains all or some
of the variables supported by this role.

It is recommended to use a *.yml* or *.yaml* extension for the
**configuration** file.

This variable is empty by default.

::

   # Using file path.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "configuration=/home/username/my-config.yml"

   # Using URL.
   ansible localhost -m include_role -a name=constrict0r.devels -K -e \
       "configuration=https://my-url/my-config.yml"

To see how to write  a configuration file see the *YAML* file format
section.
