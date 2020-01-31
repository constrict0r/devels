
Usage
*****

* To install and execute:

..

   ::

      ansible-galaxy install constrict0r.devels
      ansible localhost -m include_role -a name=constrict0r.devels -K

* Passing variables:

..

   ::

      ansible localhost -m include_role -a name=constrict0r.devels -K \
          -e "{packages: [gedit, rolldice]}"

* To include the role on a playbook:

..

   ::

      - hosts: servers
        roles:
            - {role: constrict0r.devels}

* To include the role as dependency on another role:

..

   ::

      dependencies:
        - role: constrict0r.devels
          packages: [gedit, rolldice]

* To use the role from tasks:

..

   ::

      - name: Execute role task.
        import_role:
          name: constrict0r.devels
        vars:
          packages: [gedit, rolldice]

* To run tests:

..

   ::

      cd devels
      chmod +x testme.sh
      ./testme.sh

   On some tests you may need to use *sudo* to succeed.


Developer
=========


Pytest
------

In order to run tests with pytest, execute the following steps:

* Inside your project’s root folder, create a *tests* directory:

..

   ::

      cd my-project
      mkdir tests

* Add your test file inside the *tests* folder, be sure to prefix it
   with the text *test_*, for example *test_my_test.py*.

..

   ::

      touch tests/test_my_test.py

* Inside the test file add some test functions, each function name
   must be prefixed with the text *test_*:

..

   ::

      def tests_ok():
          print('ok')

* Call pytest using the command:

..

   ::

      python3 -m pytest tests/


Pytest with virtualenv
----------------------

If you want to use a *virtualenv* for running your tests, from a
terminal:

* Activate the virtual enviroment:

..

   ::

      source bin/activate

* Then run the tests:

..

   ::

      python3 -m pytest tests/


Pytest on Emacs
---------------

On emacs, you can use the following keybindings:

* C-c C-c: Execute current script.

* C-c C-t: Execute pytest tests.

* M-x tox-run-current-test: Execute current tox test.

* M-x tox-run-current-class: Execute current tox test suite.

For more keybinding available see the `elpy documentation
<https://elpy.readthedocs.io/en/latest/>`_.


Tox
---

In order to run tox, execute the following steps:

* Create a folder named *tests*.

* Add your tests to the created folder.

* On the root directory of your project, create a *tox.ini* file with
   the following contents:

..

   ::

      [tox]
      skipsdist = True
      envlist = py{35}

      [testenv]
      deps =
        pytest
      commands =
        python3 -m pytest tests

* Finally call tox:

..

   ::

      tox


Tox on Emacs
------------

To run tox form emacs, step over the name of a test function and
execute the keybindings:

::

   M-x tox-current-test RET


Virtualenvs on Emacs
--------------------

To make emacs automatically load a virtual enviroment when a file
inside a project is edited, follow the steps:

* Create a virtual enviroment inside *·/.virtualenvs*, for example
   name it *my_virtualenv*:

..

   ::

      python3 -m venv ~/.virtualenvs/my_virtualenv

* Add a file named *.dir-locals.el* on the root directory of your
   project with the following content:

..

   ::

      ;; Directory Local Variables

      ;; Activate 'my_virtualenv' virtual enviroment from emacs.
      ((nil . ((pyvenv-workon . "my_virtualenv"))))

Now if you open a file of your project the virtual enviroment
*my_virtualenv* will be enabled automatically.


PDB on Emacs
------------

In order to run `pdb <https://docs.python.org/3/library/pdb.html>`_
from emacs when using a virtual enviroment, execute the steps:

* Create your virtual enviroment:

..

   ::

      python3 -m venv ~/.virtualenvs/my_virtualenv

* Copy **pdb3** from the system path to the newly created virtual
   enviroment:

..

   ::

      cp /usr/bin/pdb3 ~/.virtualenvs/my_virtualenv/bin/pdb

* Edit the file *~/.virtualenvs/my_virtualenv/bin/pdb* and change the
   first line from:

..

   ::

      #! /usr/bin/python3.5

* To:

..

   ::

      #! /home/username/.virtualenvs/my_virtualenv/bin/python3

* If you are developing a python package, inside emacs and on first
   editing, install your package running:

..

   ::

      M-x shell RET
      python setup.py install RET

* You can now use the following keybindings:

..

   ::

      - M-x pdb: Run PDB on a new window.
      - C-x: Set breakpoint on current line.
      - c: Run up to the breakpoint.
      - n: Next line.
      - s: Explore (search) functions on current line.
      - p: Watch a variable.
      - w: Print out the stack.
      - u: Go up on the stack.
      - d: Go down on the stack.


Poetry
------

In order to use `poetry <https://poetry.eustace.io/>`_ you will need a
**pyproject.toml** file similar to the following:

::

   [tool.poetry]
   name = "my-project"
   version = "0.1.0"
   description = "My description"
   authors = ["username <username@protonmail.com>"]
   license="MIT"

   readme = ""
   homepage="https://gitlab.com/username/my-project"
   repository="https://gitlab.com/username/my-project"
   documentation="https://project.readthedocs.io"

   keywords = ["devel", "tools"]
   classifiers = [
       'Topic :: Software Development :: Devel Tools',
       'License :: OSI Approved :: MIT License',
   ]

   [tool.poetry.dev-dependencies]
   pytest = "^3.10"
   tox = "^3.14"

   [tool.poetry.dependencies]
   click = "^7.0"
   python = "^3.7"

   [tool.poetry.scripts]
   my-project = "my_project.cli:main"

   [tool.tox]
   legacy_tox_ini= """
   [tox]
   skipsdist = True
   envlist = py{37}

   [testenv]
   deps =
     poetry
     pytest
   commands =
     poetry install
     pytest
   """
   [build-system]
   requires = ["poetry>=0.12"]
   build-backend = "poetry.masonry.api"

And then run **poetry** as a **python3** module:

::

   python3 -m poetry install


Platformio and Emacs
--------------------

To use Emacs to handle Platformio projects, follow the next steps:

Create your project directory and enter on it:

::

   mkdir ~/your-project
   cd ~/your-project

Obtain your board ID, you can use platformio to search for your board
IDE, for example, to show the boards that are compatible with the
ESP8266 microcontroller, use the following command:

::

   pio boards wemos

   # Shows something like:
   Platform: espressif8266
   -----------------------------------------------------------------------------
   ID                  MCU           Frequency  Flash   RAM    Name
   -----------------------------------------------------------------------------
   d1                  ESP8266       80Mhz     4096kB  80kB   WeMos D1(Retired)
   d1_mini             ESP8266       80Mhz     4096kB  80kB   WeMos D1 R2 & mini

For arduino you can use:

::

   pio boards arduino

   # Shows something like:
   Platform: atmelavr
   -----------------------------------------------------------------------------
   ID                  MCU           Frequency  Flash   RAM    Name
   -----------------------------------------------------------------------------
   nanoatmega328new    ATMEGA328P    16MHz      30KB    2KB     Arduino Nano
   pro16MHzatmega328   ATMEGA328P    16MHz      30KB    2KB     Arduino Pro
   robotControl        ATMEGA32U4    16MHz      28KB    2.50KB  Arduino Robot
   uno                 ATMEGA328P    16MHz      31.50KB 2KB     Arduino Uno

You can also choose your board ID by using the `platformio boards
<https://is.gd/D01WDa>`_ or the `Embedded Boards
<https://platformio.org/boards>`_ Explorer command.

Once you have your board ID, generate the project via the platformio
init **–ide command**, for example using the *d1_mini* board ID:

::

   platformio init --ide emacs --board d1_mini

Or for the Arduino Uno:

::

   platformio init --ide emacs --board uno

The **init** command will create the project structure, a
*platformio.ini* file will be created on the project’s root directory,
edit this *platformio.ini* to specify the serial port that your
microcontroller is using on your computer, it could be something like
*/dev/ttyUSB0*, */dev/ttyACM0* or similar, for the ESP8266 add:

::

   [env:d1_mini]
   platform = espressif8266
   board = d1_mini
   framework = arduino
   upload_port = /dev/ttyUSB0

For the Arduino Uno add:

::

   [env:uno]
   platform = atmelavr
   board = uno
   framework = arduino
   upload_port = /dev/ttyACM0

In order to activate the **platformio** commands on Emacs, you will
need to add a *.projectile* file on the root directory of your project
(as Emacs uses `projectile <https://github.com/bbatsov/projectile>`_
as its only requirement), create an empty *.projectile* file on root
directory:

::

   touch .projectile

Next, create the file *src/Blink.ino* with the following content and
save it:

::

   /*
   ESP8266 Blink
   Blink the blue LED on the ESP8266 module.
   */

   #define LED 2 // Define blinking LED pin.

   void setup() {
     pinMode(LED, OUTPUT); // Initialize the LED pin as an output.
   }
   // The loop function runs over and over again forever.
   void loop() {
     digitalWrite(LED, LOW); // Turn LED on (Note that LOW is the voltage level).
     delay(1000); // Wait for a second
     digitalWrite(LED, HIGH); // Turn LED off by making the voltage HIGH.
     delay(1000); // Wait for two seconds.
   }

Open the *src/Blink.ino* file with Emacs, if you are opening a *.ino*
file for the very first time, you probably have to close Emacs and
open it again to refresh the changes made by the package manager.

When Editing on Emacs, you can use the following keybindings:

* C-c i b: Build the project without auto-uploading.

* C-c i c: Clean compiled objects.

* C-c i u: Build and upload.

For more available keybindings, see the `official documentation
<https://is.gd/8HIcsb>`_.
