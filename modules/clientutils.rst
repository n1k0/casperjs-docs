==========================
The ``clientutils`` module
==========================

Casper ships with a few client-side utilities which are injected in the
remote DOM environment, and accessible from there through the
``__utils__`` object instance of the ``ClientUtils`` class of the
``clientutils`` module.

Note These tools are provided to avoid coupling CasperJS to any
third-party library like jQuery, Mootools or something; but you can
always include these and have them available client-side using the
``Casper.options.clientScripts`` option.

.. raw:: html

   <h2 id="bookmarklet">

Bookmarklet

.. raw:: html

   </h2>

A bookmarklet is also available to help injecting Casper's client-side
utilities in the DOM of your favorite browser.

Just drag this link CasperJS utils onto your favorites toobar; when
clicking, a \_\_utils\_\_ object will be available within the console of
your browser.

Note CasperJS and PhantomJS being based on Webkit, you're strongly
encouraged to use a recent Webkit compatible browser to use this
bookmarklet (Chrome, Safari, etc…)

.. raw:: html

   <h3 id="clientutils.echo">

ClientUtils#echo(String message)

.. raw:: html

   </h3>

Added in 1.0 Print a message out to the casper console from the remote
page DOM environment:

::

    casper.start('http://foo.ner/').thenEvaluate(function() {
        __utils__.echo('plop'); // this will be printed to your shell at runtime
    });

.. raw:: html

   <h3 id="clientutils.encode">

ClientUtils#encode(String contents)

.. raw:: html

   </h3>

Encodes a string using the `base64
algorithm <http://en.wikipedia.org/wiki/Base64>`_. For the records,
CasperJS doesn't use builtin ``window.btoa()`` function because it can't
deal efficiently with strings encoded using >8b characters.

::

    var base64;
    casper.start('http://foo.bar/', function() {
        base64 = this.evaluate(function() {
            return __utils__.encode("I've been a bit cryptic recently");
        });
    });

    casper.run(function() {
        this.echo(base64).exit();
    });

.. raw:: html

   <h3 id="clientutils.exists">

ClientUtils#exists(String selector)

.. raw:: html

   </h3>

Checks if a DOM element matching a given `selector
expression <selectors.html>`_ exists.

::

    var exists;
    casper.start('http://foo.bar/', function() {
        exists = this.evaluate(function() {
            return __utils__.exists('#some_id');
        });
    });

    casper.run(function() {
        this.echo(exists).exit();
    });

.. raw:: html

   <h3 id="clientutils.findAll">

ClientUtils#findAll(String selector)

.. raw:: html

   </h3>

Retrieves all DOM elements matching a given `selector
expression <selectors.html>`_.

::

    var links;
    casper.start('http://foo.bar/', function() {
        links = this.evaluate(function() {
            var elements = __utils__.findAll('a.menu');
            return Array.prototype.forEach.call(elements, function(e) {
                return e.getAttribute('href');
            });
        });
    });

    casper.run(function() {
        this.echo(JSON.stringify(links)).exit();
    });

.. raw:: html

   <h3 id="clientutils.findOne">

ClientUtils#findOne(String selector)

.. raw:: html

   </h3>

Retrieves a single DOM element by a `selector
expression <selectors.html>`_.

::

    var href;
    casper.start('http://foo.bar/', function() {
        href = this.evaluate(function() {
            return __utils__.findOne('#my_id').getAttribute('href');
        });
    });

    casper.run(function() {
        this.echo(href).exit();
    });

.. raw:: html

   <h3 id="clientutils.getBase64">

ClientUtils#getBase64(String url[, String method, Object data])

.. raw:: html

   </h3>

This method will retrieved a base64 encoded version of any resource
behind an url. For example, let's imagine we want to retrieve the base64
representation of some website's logo:

::

    var logo = null;
    casper.start('http://foo.bar/', function() {
        logo = this.evaluate(function() {
            var imgUrl = document.querySelector('img.logo').getAttribute('src');
            return __utils__.getBase64(imgUrl);
        });
    });

    casper.run(function() {
        this.echo(logo).exit();
    });

.. raw:: html

   <h3 id="clientutils.getBinary">

ClientUtils#getBinary(String url[, String method, Object data])

.. raw:: html

   </h3>

This method will retrieved the raw contents of a given binary resource;
unfortunately though, PhantomJS cannot process these data directly so
you'll have to process them within the remote DOM environment. If you
intend to download the resource, use
`ClientUtils.getBase64() <#clientutils.getBase64>`_ or
`Casper.base64encode() <api.html#casper.base64encode>`_ instead.

::

    casper.start('http://foo.bar/', function() {
        this.evaluate(function() {
            var imgUrl = document.querySelector('img.logo').getAttribute('src');
            console.log(__utils__.getBinary(imgUrl));
        });
    });

    casper.run();

.. raw:: html

   <h3 id="clientutils.getDocumentHeight">

ClientUtils#getDocumentHeight()

.. raw:: html

   </h3>

Added in 1.0 Retrieves current document height.

::

    var documentHeight;

    casper.start('http://google.com/', function() {
        documentHeight = this.evaluate(function() {
            return __utils__.getDocumentHeight();
        });
        this.echo('Document height is ' + documentHeight + 'px');
    });

    casper.run();

.. raw:: html

   <h3 id="clientutils.getElementBounds">

Casper#getElementBounds(String selector)

.. raw:: html

   </h3>

Retrieves boundaries for a DOM element matching the provided
`selector <selectors.html>`_.

It returns an Object with four keys: ``top``, ``left``, ``width`` and
``height``, or ``null`` if the selector doesn't exist.

.. raw:: html

   <h3 id="clientutils.getElementsBounds">

Casper#getElementsBounds(String selector)

.. raw:: html

   </h3>

Retrieves boundaries for all DOM element matching the provided
`selector <selectors.html>`_.

It returns an array of objects each having four keys: ``top``, ``left``,
``width`` and ``height``.

.. raw:: html

   <h3 id="clientutils.getElementByXPath">

ClientUtils#getElementByXPath(String expression [, HTMLElement scope])

.. raw:: html

   </h3>

Retrieves a single DOM element matching a given `XPath
expression <http://www.w3.org/TR/xpath/>`_.

Added in 1.0 The ``scope`` argument allow to set the context for
executing the XPath query:

::

    // will be performed against the whole document
    __utils__.getElementByXPath('.//a');

    // will be performed against a given DOM element
    __utils__.getElementByXPath('.//a', __utils__.findOne('div.main'));

.. raw:: html

   <h3 id="clientutils.getElementsByXPath">

ClientUtils#getElementsByXPath(String expression [, HTMLElement scope])

.. raw:: html

   </h3>

Retrieves all DOM elements matching a given `XPath
expression <http://www.w3.org/TR/xpath/>`_, if any.

Added in 1.0 The ``scope`` argument allow to set the context for
executing the XPath query.

.. raw:: html

   <h3 id="clientutils.getFieldValue">

ClientUtils#getFieldValue(String inputName)

.. raw:: html

   </h3>

Added in 1.0 Retrieves the value from the field named against the
``inputNamed`` argument:

**Example:**

::

    <form>
        <input type="text" name="plop" value="42">
    </form>

::

    __utils__.getFieldValue('plop'); // 42

.. raw:: html

   <h3 id="clientutils.getFormValues">

ClientUtils#getFormValues(String selector)

.. raw:: html

   </h3>

Added in 1.0 Retrieves a given form all of its field values.

**Example:**

::

    <form id="login" action="/login">
        <input type="text" name="username" value="foo">
        <input type="text" name="password" value="bar">
        <input type="submit">
    </form>

::

    __utils__.getFormValues('form#login'); // {username: 'foo', password: 'bar'}

.. raw:: html

   <h3 id="clientutils.mouseEvent">

ClientUtils#mouseEvent(String type, String selector)

.. raw:: html

   </h3>

Dispatches a mouse event to the DOM element behind the provided
selector.

Supported events are ``mouseup``, ``mousedown``, ``click``,
``mousemove``, ``mouseover`` and ``mouseout``.

.. raw:: html

   <h3 id="clientutils.removeElementsByXPath">

ClientUtils#removeElementsByXPath(String expression)

.. raw:: html

   </h3>

Removes all DOM elements matching a given `XPath
expression <http://www.w3.org/TR/xpath/>`_.

.. raw:: html

   <h3 id="clientutils.sendAJAX">

ClientUtils#sendAJAX(String url[, String method, Object data, Boolean
async])

.. raw:: html

   </h3>

Added in 1.0 Sends an AJAX request, using the following parameters:

-  ``url``: The url to request.
-  ``method``: The HTTP method (default: ``GET``).
-  ``data``: Request parameters (default: ``null``).
-  ``async``: Flag for an asynchroneous request? (default: ``false``)

Caveat Don't forget to pass the ``--web-security=no`` option in your CLI
call in order to perform cross-domains requests when needed.

Sample usage:

::

    var data, wsurl = 'http://api.site.com/search.json';

    casper.start('http://my.site.com/', function() {
        data = this.evaluate(function(wsurl) {
            return JSON.parse(__utils__.sendAJAX(wsurl, 'GET', null, false));
        }, {wsurl: wsurl});
    });

    casper.then(function() {
        require('utils').dump(data);
    });

.. raw:: html

   <h3 id="clientutils.visible">

ClientUtils#visible(String selector)

.. raw:: html

   </h3>

Checks if an element is visible.

::

    var logoIsVisible = casper.evaluate(function() {
        return __utils__.visible('h1');
    });

