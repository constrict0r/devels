
Attributes
**********

On the item level you can use attributes to configure how this role
handles the items data.

The attributes supported by this role are:


item_name
=========

Name of the item to load or create.

::

   ---
   packages:
     - item_name: my-item-name


item_pass
=========

Password for the item to load or create.

::

   ---
   packages:
     - item_pass: my-item-pass


item_groups
===========

List of groups to add users into.

::

   ---
   packages:
     - item_name: my-username
       item_groups: [disk, sudo]


item_expand
===========

Boolean value indicating if treat this item as a file path or URL or
just treat it as plain text.

::

   ---
   packages:
     - item_expand: true
       item_path: /home/username/my-config.yml


item_path
=========

Absolute file path or URL to a *.yml* file.

::

   ---
   packages:
     - item_path: /home/username/my-config.yml

This attribute also works with URLs.
