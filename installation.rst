.. _installation:

============
Installation
============

.. topic:: CasperJS is based on PhantomJS

   PhantomJS_ >= 1.7 must be installed on your system.

   Check out `PhantomJS' installation instructions <http://phantomjs.org/download.html>`_, and:

   -  Ensure to always install the **latest stable version of PhantomJS**;
   -  **Ubuntu users:** double check the version of PhantomJS provided by your apt repository, if any. Often, only old versions are provided.

.. note::

   The ``casperjs`` executable is written in `Python <http://python.org/>`_, so please ensure that a Python interpreter is available on your platform.

Installing from Homebrew  (OSX)
-------------------------------

Installation of both PhantomJS and CasperJS can be achieved through `Homebrew <http://mxcl.github.com/homebrew/>`_::

   $ brew install casperjs

Installing from git
-------------------

Installation can be achieved using `git <http://git-scm.com/>`_::

    $ git clone git://github.com/n1k0/casperjs.git
    $ cd casperjs
    $ git checkout tags/1.1
    $ ln -sf `pwd`/bin/casperjs /usr/local/bin/casperjs

Once PhantomJS and CasperJS installed on your machine, you should obtain
something like this::

    $ phantomjs --version
    1.7
    $ casperjs --version
    1.1

You are now ready to write your `first script <quickstart.html>`_!

Ruby version
~~~~~~~~~~~~

.. versionadded:: 1.0

A `Ruby <http://ruby-lang.org/>`_ version of the ``casperjs`` executable is also available in the ``rubybin/`` directory; in order to use the Ruby version instead of the Python one::

    $ ln -sf `pwd`/rubybin/casperjs /usr/local/bin/casperjs

Or using the ruby interpreter::

    $ ruby /path/to/casperjs/rubybin/casperjs
    CasperJS version 1.1 at /Users/niko/Sites/casperjs, using PhantomJS version 1.7.0
    ...

CasperJS on Windows
-------------------

Phantomjs installation additions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Append ``";C:\phantomjs"`` to your ``PATH`` environment variable.
- Modify this path appropriately if you installed PhantomJS to a different location.

Casperjs installation additions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. versionadded:: 1.0

CasperJS, as of 1.0.0-RC3, ships with a Batch script so you don't need Python nor Ruby to use it.

- Append ``";C:\casperjs\batchbin"`` to your ``PATH`` environment variable.
- Modify this path appropriately if you installed CasperJS to a different location.

You can now run any regular casper scripts that way::

    C:> casperjs.bat myscript.js

Earlier versions of CasperJS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before 1.0.0-RC3, you had to setup your casper scripts that way::

    phantom.casperPath = 'C:\\casperjs-1.1';
    phantom.injectJs(phantom.casperPath + '\\bin\\bootstrap.js');

    var casper = require('casper').create();

    // do stuff

Run the script using the ``phantom.exe`` program::

    C:> phantomjs.exe myscript.js

.. note::

   There is no output coloration when running CasperJS on Microsoft platforms.

Known Bugs & Limitations
------------------------

- Due to its asynchronous nature, CasperJS doesn't work well with `PhantomJS' REPL <http://code.google.com/p/phantomjs/wiki/InteractiveModeREPL>`_.

.. _PhantomJS: http://phantomjs.org/
