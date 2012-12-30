============
Installation
============

.. topic:: CasperJS is based on PhantomJS
   `PhantomJS <http://phantomjs.org/>`_ >= 1.7 must be installed on your system.

   Check out `PhantomJS' installation instructions <http://code.google.com/p/phantomjs/wiki/Installation>`_, and:

   -  Ensure to always install the **latest stable version of PhantomJS**;
   -  **Ubuntu users:** double check the version of PhantomJS provided by your apt repository, if any. Often, only old versions are provided.

Installing from Homebrew  (OSX)
-------------------------------

Installation of both PhantomJS and CasperJS can be achieved through `Homebrew <http://mxcl.github.com/homebrew/>`_::

   $ brew install casperjs

Installing from git
-------------------

Installation can be achieved using `git <http://git-scm.com/>`_::

    $ git clone git://github.com/n1k0/casperjs.git
    $ cd casperjs
    $ git checkout tags/{{version}}
    $ ln -sf `pwd`/bin/casperjs /usr/local/bin/casperjs

Version checking
----------------

Once PhantomJS and CasperJS installed on your machine, you should obtain
something like this::

    $ phantomjs --version
    1.7
    $ casperjs --version
    {{version}}

You are now ready to write your `first script <quickstart.html>`_!

Note The ``casperjs`` executable is written in
`Python <http://python.org/>`_, so please ensure that a Python
interpreter is available on your platform.

Ruby version
~~~~~~~~~~~~

Added in 1.0 A `Ruby <http://ruby-lang.org/>`_ version of the ``casperjs`` executable is also available in the ``rubybin/`` directory; in order to use the ruby version instead of the python one::

    $ ln -sf `pwd`/rubybin/casperjs /usr/local/bin/casperjs

Or using the ruby interpreter::

    $ ruby /path/to/casperjs/rubybin/casperjs
    CasperJS version {{version}} at /Users/niko/Sites/casperjs, using PhantomJS version 1.7.0
    ...

CasperJS on Windows
-------------------

Phantomjs installation additions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Append ``";C:\phantomjs"`` to your ``PATH`` environment variable.
- Modify this path appropriately if you installed PhantomJS to a different location.

Casperjs installation additions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Added in 1.0 CasperJS, as of 1.0.0-RC3, ships with a Batch script so you don't need Python nor Ruby to use it.

- Append ``";C:\casperjs\batchbin"`` to your ``PATH`` environment variable.
- Modify this path appropriately if you installed CasperJS to a different location.

You can now run any regular casper scripts that way::

    C:> casperjs.bat myscript.js

Earlier versions of CasperJS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before 1.0.0-RC3, you had to setup your casper scripts that way::

    phantom.casperPath = 'C:\\casperjs-{{version}}';
    phantom.injectJs(phantom.casperPath + '\\bin\\bootstrap.js');

    var casper = require('casper').create();

    // do stuff

Run the script using the ``phantom.exe`` program::

    C:> phantomjs.exe myscript.js

Note There is no output coloration when running CasperJS on Microsoft
platforms.

Known Bugs & Limitations
------------------------

- Due to its asynchronous nature, CasperJS doesn't work well with PhantomJS' REPL.
