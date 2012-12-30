.. _testing:

=======
Testing
=======

Hint If you intend to write large test suites, check out the `casperjs test command`_.

CasperJS ships with a handful set of tools to be used as a functional testing framework. For example, let's test write a tests suite for testing google search (yes, you read it well)::

    var casper = require('casper').create();

    casper.start('http://www.google.fr/', function() {
        this.test.assertTitle('Google', 'google homepage title is the one expected');
        this.test.assertExists('form[action="/search"]', 'main form is found');
        this.fill('form[action="/search"]', {
            q: 'foo'
        }, true);
    });

    casper.then(function() {
        this.test.assertTitle('foo - Recherche Google', 'google title is ok');
        this.test.assertUrlMatch(/q=foo/, 'search term has been submitted');
        this.test.assertEval(function() {
            return __utils__.findAll('h3.r').length >= 10;
        }, 'google search for "foo" retrieves 10 or more results');
    });

    casper.run(function() {
        this.test.done(5); // checks that 5 assertions have been executed
        this.test.renderResults(true);
    });

As you can see, the ``test`` propery of the ``casper`` object is a reference to a :ref:`tester module <tester_module>` object, which is used to execute the assertions and renders the results.

Note You can find the whole ``tester.Tester`` API documentation in the `dedicated section <api.html#tester>`_.

Now run the tests suite:

.. code-block:: text

    $ casperjs samples/googletesting.js

You'll probably get something like this:

.. figure:: _static/images/testsuiteok.png
   :align: center
   :alt: capture

   capture

In case any assertion fails, you'd rather get something like the following:

.. figure:: _static/images/testsuitefail.png
   :align: center
   :alt: capture

   capture


Exporting results in *XUnit* format
-----------------------------------

CasperJS can export the results of the test suite to an XUnit XML file, which is compatible with continuous integration tools such as `Jenkins <http://jenkins-ci.org/>`_. To save the XUnit log of your test suite to a ``log.xml`` file, you can process this way::

    casper.run(function() {
        this.test.renderResults(true, 0, 'log.xml');
    });

A cooler way is to add an option to your script using CLI argument parsing::

    casper.run(function() {
        this.test.renderResults(true, 0, this.cli.get('save') || false);
    });

Then you can run:

.. code-block:: text

    $ casperjs test.js --save=log.xml


``casperjs test`` command
-------------------------

Writing all your tests in a single file may be painful, to say the
least. That's where the ``casperjs test`` command comes to the rescue,
as it allows to split your tests across different files among other
handy little things.

Let's take this first test file as an example::

    // file: /path/to/test/dir/test1.js

    casper.test.comment('My first test file');
    casper.test.assert(true, "true is so true");
    casper.test.assertNot(false, "false is wrong");
    casper.test.done(2); // I must be called, and I'll check that
                         // two assertions have been executed

And this second one::

    // file: /path/to/test/dir/test2.js

    casper.test.comment('This is my second test file, a bit more async');

    casper.start('http://my.location.tld/', function() {
        this.test.assertNot(false, "false is so false");
    });

    casper.run(function() {
        this.test.done(1); // I must be called once all the async stuff
                           // has been executed. I'll also check that a
                           // single assertions has been performed.
    });

Note The ``expected`` parameter of ``Tester.done()`` has been added in
1.0.

Now let's run our test suite using ``casperjs test``:

.. code-block:: text

    $ casperjs test /path/to/test/dir/

This is theoretically what you will get:

.. figure:: _static/images/split-test-results.png
   :align: center
   :alt: image

   image

Also, you can of course run a single test file as well:

.. code-block :: text

    $ casperjs test /path/to/test/dir/test1.js

.. warning ::

   There are two important conditions for splitting your test suite across several files:

   - Not to create a new Casper instance in a split test file;
   - To call the Tester.done() method when all the tests contained in a single file have been executed.

Options
~~~~~~~

Some options are available using the ``casperjs test`` command:

- ``--xunit=<filename>`` will export test suite results in a XUnit XML file
- ``--direct`` will output log messages directly to the console
- ``--log-level=<logLevel>`` sets the logging level (see the :doc:`related section <logging>`)

.. versionadded:: 1.0.0

- ``--includes=foo.js,bar.js`` will includes the ``foo.js`` and  ``bar.js`` files before each test file execution
- ``--pre=pre-test.js`` will add th e tests contained in ``pre- test.js`` **before** executing the test suite
- ``--post=post-test.js`` will add the tests contained in ``po st -test.js`` **after** having executed the whole test suite
- ``--fail-fast`` will terminate the current test suite as soon as a first failure is encountered.

Sample custom command:

.. code-block:: text

    $ casperjs test --includes=foo.js,bar.js \
                    --pre=pre-test.js \
                    --post=post-test.js \
                    --direct \
                    --log-level=debug \
                    --fail-fast \
                    test1.js test2.js /path/to/some/test/dir

.. hint::

   A `demo gist <https://gist.github.com/3813361>`_ is also available in order to get you started with a sample suite involving some of these options.

CasperJS own test suite
~~~~~~~~~~~~~~~~~~~~~~~

CasperJS has its own unit and functional test suite, located in the ``tests`` subfolder. To run this test suite:

.. code-block:: text

    $ cd /path/to/casperjs
    $ casperjs selftest

.. note::

   Running this test suite is a great way to find any bug on your platform. If it fails, feel free to `file an issue <https://github.com/n1k0/casperjs/issues/new>`_ or to ask on the `CasperJS mailing-list <https://groups.google.com/forum/#!forum/casperjs>`_.

--------------

Extending Casper for Testing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This command:

.. code-block:: text

    $ casperjs test [path]

is just a shortcut for this one:

.. code-block:: text

    $ casper /path/to/casperjs/tests/run.js [path]

So if you want to extend Casper capabilities for your tests, your best bet is to write your own runner and extend the casper object instance from there.

.. hint::

   You can find the default runner code in `run.js <https://github.com/n1k0/casperjs/blob/master/tests/run.js>`_.
