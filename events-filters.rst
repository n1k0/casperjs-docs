.. _events_filters:

Events & filters
================

CasperJS provides an `event handler <#events>`_ very similar to the `nodejs <http://nodejs.org>`_' `one <https://github.com/joyent/node/blob/master/lib/events.js>`_; actually it borrows most of its codebase. CasperJS also adds `filters <#filters>`_, which are basically ways to alter values asynchronously.


Events
------

Using events is pretty much straightforward if you're a node developer, or if you worked with any evented system before::

    var casper = require('casper').create();

    casper.on('resource.received', function(resource) {
        casper.echo(resource.url);
    });

Emitting you own events
+++++++++++++++++++++++

Of course you can emit your own events, using the ``Casper.emit()`` method:

::

    var casper = require('casper').create();

    // listening to a custom event
    casper.on('google.loaded', function() {
        this.echo('Google page title is ' + this.getTitle());
    });

    casper.start('http://google.com/', function() {
        // emitting a custom event
        this.emit('google.loaded');
    });

    casper.run();

Events reference
++++++++++++++++

``back``
~~~~~~~~

**Arguments:** ``None``

Emitted when the embedded browser is asked to go back a step in its
history.

``capture.saved``
~~~~~~~~~~~~~~~~~

**Arguments:** ``targetFile``

Emitted when a screenshot image has been captured.

``click``
~~~~~~~~~

**Arguments:** ``selector``

Emitted when the ``Casper.click()`` method has been called.

``die``
~~~~~~~

**Arguments:** ``message, status``

Emitted when the ``Casper.die()`` method has been called.

``downloaded.file``
~~~~~~~~~~~~~~~~~~~

**Arguments:** ``targetPath``

Emitted when a file has been downloaded by ```Casper.download()`` <api.html#casper.download>`_; ``target`` will contain the path to the downloaded file.

``error``
~~~~~~~~~

**Arguments:** ``msg, backtrace``

.. note:: Added in 0.6.9

Emitted when an error hasn't been caught. Do basically what PhantomJS' ``onError()`` native handler does.

``exit``
~~~~~~~~

**Arguments:** ``status``

Emitted when the ``Casper.exit()`` method has been called.

``fill``
~~~~~~~~

**Arguments:** ``selector, vals, submit``

Emitted when a form is filled using the ``Casper.fill()`` method.

``forward``
~~~~~~~~~~~

**Arguments:** ``None``

Emitted when the embedded browser is asked to go forward a step in its history.

``http.auth``
~~~~~~~~~~~~~

**Arguments:** ``username, password``

Emitted when http authentication parameters are set.

``http.status.[code]``
~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``resource``

Emitted when any given HTTP reponse is received with the status code specified by ``[code]``, eg.:

::

    casper.on('http.status.404', function(resource) {
        casper.echo(resource.url + ' is 404');
    })

``load.started``
~~~~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when PhantomJS' ``WebPage.onLoadStarted`` event callback is called.

``load.failed``
~~~~~~~~~~~~~~~

**Arguments:** ``Object``

Emitted when PhantomJS' ``WebPage.onLoadFinished`` event callback has been called and failed.

``load.finished``
~~~~~~~~~~~~~~~~~

**Arguments:** ``status``

Emitted when PhantomJS' ``WebPage.onLoadFinished`` event callback is called.

``log``
~~~~~~~

**Arguments:** ``entry``

Emitted when the ``Casper.log()`` method has been called. The ``entry`` parameter is an Object like this:

::

    {
        level:   "debug",
        space:   "phantom",
        message: "A message",
        date:    "a javascript Date instance"
    }

``mouse.click``
~~~~~~~~~~~~~~~

**Arguments:** ``args``

Emitted when the mouse left-click something or somewhere.

``mouse.down``
~~~~~~~~~~~~~~

**Arguments:** ``args``

Emitted when the mouse presses on something or somewhere with the left button.

``mouse.move``
~~~~~~~~~~~~~~

**Arguments:** ``args``

Emitted when the mouse moves onto something or somewhere.

``mouse.up``
~~~~~~~~~~~~

**Arguments:** ``args``

Emitted when the mouse releases the left button over something or somewhere.

``navigation.requested``
~~~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``url, navigationType, navigationLocked, isMainFrame``

.. note:: Added in 1.0

Emitted each time a navigation operation has been requested. Available navigation types are: ``LinkClicked``, ``FormSubmitted``, ``BackOrForward``, ``Reload``, ``FormResubmitted`` and ``Other``.

``open``
~~~~~~~~

``location, settings``

Emitted when an HTTP request is sent. First callback arg is the location, second one is a request settings Object of the form:

::

    {
        method: "post",
        data:   "foo=42&chuck=norris"
    }

``page.created``
~~~~~~~~~~~~~~~~

**Arguments:** ``page``

Emitted when PhantomJS' ``WebPage`` object used by CasperJS has been created.

``page.error``
~~~~~~~~~~~~~~

**Arguments:** ``message, trace``

Emitted when retrieved page leaved a Javascript error uncaught:

::

    casper.on("page.error", function(msg, trace) {
        this.echo("Error: " + msg, "ERROR");
    });

``page.initialized``
~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``WebPage``

Emitted when PhantomJS' ``WebPage`` object used by CasperJS has been initialized.

``page.resource.received``
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``response``

Emitted when the HTTP response corresponding to current required url has been received.

``page.resource.requested``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``request``

Emitted when a new HTTP request is performed to open the required url.

``popup.created``
~~~~~~~~~~~~~~~~~

**Arguments:** ``WebPage``

Emitted when a new window has been opened.

``popup.loaded``
~~~~~~~~~~~~~~~~

**Arguments:** ``WebPage``

Emitted when a new window has been loaded.

``popup.closed``
~~~~~~~~~~~~~~~~

**Arguments:** ``WebPage``

Emitted when a new opened window has been closed.

``popup.created``
~~~~~~~~~~~~~~~~~

**Arguments:** ``WebPage``

Emitted when a new window has been opened.

``remote.alert``
~~~~~~~~~~~~~~~~

**Arguments:** ``message``

Emitted when a remote ``alert()`` call has been performed.

``remote.message``
~~~~~~~~~~~~~~~~~~

**Arguments:** ``msg``

Emitted when any remote console logging call has been performed.

``resource.received``
~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``resource``

Emitted when any resource has been received.

``resource.requested``
~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``request``

Emitted when any resource has been requested.

``run.complete``
~~~~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when the whole series of steps in the stack have been executed.

``run.start``
~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when ``Casper.run()`` is called.

``starting``
~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when ``Casper.start()`` is called.

``started``
~~~~~~~~~~~

**Arguments:** ``None``

Emitted when Casper has been started using ``Casper.start()``.

``step.added``
~~~~~~~~~~~~~~

**Arguments:** ``step``

Emitted when a new navigation step has been added to the stack.

``step.complete``
~~~~~~~~~~~~~~~~~

**Arguments:** ``stepResult``

Emitted when a navigation step has been executed.

``step.created``
~~~~~~~~~~~~~~~~

**Arguments:** ``fn``

Emitted when a new navigation step has been created.

``step.start``
~~~~~~~~~~~~~~

**Arguments:** ``step``

Emitted when a navigation step has been started.

``step.timeout``
~~~~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when a navigation step has been executed.

``timeout``
~~~~~~~~~~~

**Arguments:** ``None``

Emitted when the execution time of the script has reached the ``Casper.options.timeout`` value.

``url.changed``
~~~~~~~~~~~~~~~

**Arguments:** ``url``

Added in 1.0 Emitted each time the current page url changes.

``viewport.changed``
~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``[width, height]``

Emitted when the viewport has been changed.

``wait.done``
~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when a ``Casper.wait()``\ *operation ends.*

``wait.start``
~~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when a ``Casper.wait()`` operation starts.

``waitFor.timeout``
~~~~~~~~~~~~~~~~~~~

**Arguments:** ``None``

Emitted when the execution time of a ``Casper.wait*()`` operation has exceeded the value of ``Casper.options.stepTimeout``.


Filters
-------

Filters allow you to alter some values asynchronously. Sounds obscure? Let's take a simple example and imagine you would like to alter every single url opened by CasperJS to append a ``foo=42`` query string parameter:

::

    var casper = require('casper').create();

    casper.setFilter('open.location', function(location) {
        return /\?+/.test(location) ? location += "&foo=42" : location += "?foo=42";
    });

There you have it, every single requested url will have this appended. Let me bet you'll find far more interesting use cases than my silly one ;)

Here'a the list of all available filters with their expected return value:

Filters reference
+++++++++++++++++

``capture.target_filename``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Arguments:** ``args``

**Return type:** ``String``

Allows to alter the value of the filename where a screen capture should be stored.

``echo.message``
~~~~~~~~~~~~~~~~

**Arguments:** ``message``

**Return type:** ``String``

Allows to alter every message written onto stdout.

``log.message``
~~~~~~~~~~~~~~~

**Arguments:** ``message``

**Return type:** ``String``

Allows to alter every log message.

``open.location``
~~~~~~~~~~~~~~~~~

**Arguments:** ``args``

**Return type:** ``String``

Allows to alter every url before it being opened.

``page.confirm``
~~~~~~~~~~~~~~~~

**Arguments:** ``message``

**Return type:** ``Boolean``

.. note:: Added in 1.0

Allows to react on a javascript ``confirm()`` call:

::

    casper.setFilter("page.confirm", function(msg) {
        return msg === "Do you like vbscript?" ? false : true;
    });

``page.prompt``
~~~~~~~~~~~~~~~

**Arguments:** ``message, value``

**Return type:** ``String``

.. note:: Added in 1.0

Allows to react on a javascript ``prompt()`` call:

::

    casper.setFilter("page.prompt", function(msg, value) {
        if (msg === "What's your name?") {
            return "Chuck";
        }
    });
