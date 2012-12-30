=====================
The ``casper`` module
=====================

The Casper class
----------------

The most easy way to instantiate a casper instance is to use the
module's ``create()`` method:

::

    var casper = require('casper').create();

But you can also retrieve the main Function and instantiate it by
yourself:

::

    var casper = new require('casper').Casper();

Hint Also, check out `how to extend Casper with your own
methods <extending.html>`_.

.. raw:: html

   <h3 id="casper.options">

Casper([Object options])

.. raw:: html

   </h3>

Both the ``Casper`` constructor and the ``create()`` function accept a
single ``options`` argument which is a standard javascript object:

::

    var casper = require('casper').create({
        verbose: true,
        logLevel: "debug"
    });

Casper options
--------------

All the available options are detailed below:

.. raw:: html

   <table class="table table-striped table-condensed" caption="Casper options">
     <thead>
       <tr>
         <th>

Name

.. raw:: html

   </th>
         <th>

Type

.. raw:: html

   </th>
         <th>

Default

.. raw:: html

   </th>
         <th>

Description

.. raw:: html

   </th>
       </tr>
     </thead>
     <tbody>
       <tr>
         <td>

clientScripts

.. raw:: html

   </td>
         <td>

Array

.. raw:: html

   </td>
         <td>

[]

.. raw:: html

   </td>
         <td>


A collection of script filepaths to include to every page loaded

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

exitOnError

.. raw:: html

   </td>
         <td>

Boolean

.. raw:: html

   </td>
         <td>

true

.. raw:: html

   </td>
         <td>


Sets if CasperJS must exit when an uncaught error has been thrown by the
script.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

httpStatusHandlers

.. raw:: html

   </td>
         <td>

Object

.. raw:: html

   </td>
         <td>

{}

.. raw:: html

   </td>
         <td>


A javascript Object containing functions to call when a requested
resource has a given HTTP status code. A dedicated sample is provided as
an example.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

logLevel

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>

"error"

.. raw:: html

   </td>
         <td>


Logging level (see the logging section for more information)

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onAlert

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


A function to be called when a javascript alert() is triggered

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onDie

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


A function to be called when Casper#die() is called

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onError

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


A function to be called when an "error" level event occurs

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onLoadError

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


A function to be called when a requested resource cannot be loaded

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onPageInitialized

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

A function to be called after WebPage instance has been initialized

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onResourceReceived

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


Proxy method for PhantomJS' WebPage#onResourceReceived() callback, but
the current Casper instance is passed as first argument.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onResourceRequested

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>


Proxy method for PhantomJS' WebPage#onResourceRequested() callback, but
the current Casper instance is passed as first argument.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onStepComplete

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

A function to be executed when a step function execution is finished.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

onStepTimeout

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>
           <p>

A function to be executed when a step function execution time exceeds
the value of the stepTimeout option, if any has been set.

.. raw:: html

   </p>
           <p>

By default, on timeout the script will exit displaying an error, except
in test environment where it will just add a failure to the suite
results.

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

onTimeout

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>
           <p>

A function to be executed when script execution time exceeds the value
of the timeout option, if any has been set.

.. raw:: html

   </p>
           <p>

By default, on timeout the script will exit displaying an error, except
in test environment where it will just add a failure to the suite
results.

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

onWaitTimeout

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>

Function

.. raw:: html

   </td>
         <td>
           <p>

A function to be executed when a waitFor\* function execution time
exceeds the value of the waitTimeout option, if any has been set.

.. raw:: html

   </p>
           <p>

By default, on timeout the script will exit displaying an error, except
in test environment where it will just add a failure to the suite
results.

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

page

.. raw:: html

   </td>
         <td>

WebPage

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

An existing WebPage instance

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

pageSettings

.. raw:: html

   </td>
         <td>

Object

.. raw:: html

   </td>
         <td>

{}

.. raw:: html

   </td>
         <td>
           <p>


PhantomJS's WebPage settings object. Available settings are:

.. raw:: html

   </p>
           <ul>
             <li>


javascriptEnabled defines whether to execute the script in the page or
not (default to true)

.. raw:: html

   </li>
             <li>


loadImages defines whether to load the inlined images or not

.. raw:: html

   </li>
             <li>


loadPlugins defines whether to load NPAPI plugins (Flash, Silverlight,
...) or not

.. raw:: html

   </li>
             <li>


localToRemoteUrlAccessEnabled defines whether local resource (e.g. from
file) can access remote URLs or not (default to false)

.. raw:: html

   </li>
             <li>


userAgent defines the user agent sent to server when the web page
requests resources.

.. raw:: html

   </li>
             <li>


userName sets the user name used for HTTP authentication

.. raw:: html

   </li>
             <li>


password sets the password used for HTTP authentication

.. raw:: html

   </li>
             <li>


XSSAuditingEnabled defines whether load requests should be monitored for
cross-site scripting attempts (default to false)

.. raw:: html

   </li>
           </ul>
         </td>
       </tr>
       <tr>
         <td>

remoteScripts

.. raw:: html

   </td>
         <td>

Array

.. raw:: html

   </td>
         <td>

[]

.. raw:: html

   </td>
         <td>
           <p>

Added in 1.0

.. raw:: html

   </p>
           <p>

A collection of remote script urls to include to every page loaded

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

safeLogs

.. raw:: html

   </td>
         <td>

Boolean

.. raw:: html

   </td>
         <td>

true

.. raw:: html

   </td>
         <td>


Added in 1.0 When this option is set to true — which is the default, any
password information entered in <input type="password"> will be
obfuscated in log messages. Set safeLogs to false to disclose passwords
in plain text (not recommended).

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

stepTimeout

.. raw:: html

   </td>
         <td>

Number

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

Max step timeout in milliseconds; when set, every defined step function
will have to execute before this timeout value has been reached. You can
define the onStepTimeout() callback to catch such a case. By default,
the script will die() with an error message.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

timeout

.. raw:: html

   </td>
         <td>

Number

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

Max timeout in milliseconds

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

verbose

.. raw:: html

   </td>
         <td>

Boolean

.. raw:: html

   </td>
         <td>

false

.. raw:: html

   </td>
         <td>

Realtime output of log messages

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

viewportSize

.. raw:: html

   </td>
         <td>

Object

.. raw:: html

   </td>
         <td>

null

.. raw:: html

   </td>
         <td>

Viewport size, eg. {width: 800, height: 600}

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

waitTimeout

.. raw:: html

   </td>
         <td>

Number

.. raw:: html

   </td>
         <td>

5000

.. raw:: html

   </td>
         <td>

Default wait timeout, for wait\* family functions.

.. raw:: html

   </td>
       </tr>
     </tbody>
   </table>

**Example:**

::

    var casper = require('casper').create({
        clientScripts:  [
            'includes/jquery.js',      // These two scripts will be injected in remote
            'includes/underscore.js'   // DOM on every request
        ],
        logLevel: "info",              // Only "info" level messages will be logged
        onError: function(self, m) {   // Any "error" level message will be written
            console.log('FATAL:' + m); // on the console output and PhantomJS will
            self.exit();               // terminate
        },
        pageSettings: {
            loadImages:  false,        // The WebPage instance used by Casper will
            loadPlugins: false         // use these settings
        }
    });

But no worry, usually you'll just need to instantiate Casper using
``require('casper').create()``.

.. raw:: html

   <h3 id="casper.back">

Casper#back()

.. raw:: html

   </h3>

Moves back a step in browser's history.

::

    casper.start('http://foo.bar/1')
    casper.thenOpen('http://foo.bar/2');
    casper.thenOpen('http://foo.bar/3');
    casper.back();
    casper.run(function() {
        console.log(this.getCurrentUrl()); // 'http://foo.bar/2'
    });

Also have a look at ```Casper.forward()`` <#forward>`_.

.. raw:: html

   <h3 id="casper.base64encode">

Casper#base64encode(String url [, String method, Object data])

.. raw:: html

   </h3>

Encodes a resource using the base64 algorithm synchronously using
client-side XMLHttpRequest.

Note We cannot use ``window.btoa()`` because it fails miserably in the
version of WebKit shipping with PhantomJS.

Example: retrieving google logo image encoded in base64:

::

    var base64logo = null;
    casper.start('http://www.google.fr/', function() {
        base64logo = this.base64encode('http://www.google.fr/images/srpr/logo3w.png');
    });

    casper.run(function() {
        this.echo(base64logo).exit();
    });

You can also perform an HTTP POST request to retrieve the contents to
encode:

::

    var base46contents = null;
    casper.start('http://domain.tld/download.html', function() {
        base46contents = this.base64encode('http://domain.tld/', 'POST', {
            param1: 'foo',
            param2: 'bar'
        });
    });

::

    casper.run(function() {
        this.echo(base46contents).exit();
    });

.. raw:: html

   <h3 id="casper.click">

Casper#click(String selector)

.. raw:: html

   </h3>

Performs a click on the element matching the provided `selector
expression <selectors.html>`_. The method tries two strategies
sequentially:

1. trying to trigger a MouseEvent in Javascript
2. using native QtWebKit event if the previous attempt failed

Example:

::

    casper.start('http://google.fr/');

    casper.thenEvaluate(function(term) {
        document.querySelector('input[name="q"]').setAttribute('value', term);
        document.querySelector('form[name="f"]').submit();
    }, { term: 'CasperJS' });

    casper.then(function() {
        // Click on 1st result link
        this.click('h3.r a');
    });

    casper.then(function() {
        console.log('clicked ok, new location is ' + this.getCurrentUrl());
    });

    casper.run();

.. raw:: html

   <h3 id="casper.clickLabel">

Casper#clickLabel(String label[, String tag])

.. raw:: html

   </h3>

Added in 0.6.10 Clicks on the first DOM element found containing
``label`` text. Optionaly ensures that the element node name is ``tag``.

::

    // <a href="...">My link is beautiful</a>
    casper.then(function() {
        this.clickLabel('My link is beautiful', 'a');
    });

    // <button type="submit">But my button is sexier</button>
    casper.then(function() {
        this.clickLabel('But my button is sexier', 'button');
    });

.. raw:: html

   <h3 id="casper.capture">

Casper#capture(String targetFilepath, Object clipRect)

.. raw:: html

   </h3>

Proxy method for PhantomJS' ``WebPage#render``. Adds a clipRect
parameter for automatically setting page clipRect setting values and
sets it back once done.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.capture('google.png', {
            top: 100,
            left: 100,
            width: 500,
            height: 400
        });
    });

    casper.run();

.. raw:: html

   <h3 id="casper.captureBase64">

Casper#captureBase64(String format[, Mixed area])

.. raw:: html

   </h3>

Added in 0.6.5 Computes the
`Base64 <http://en.wikipedia.org/wiki/Base64>`_ representation of a
binary image capture of the current page, or an area within the page, in
a given format.

Supported image formats are ``bmp``, ``jpg``, ``jpeg``, ``png``,
``ppm``, ``tiff``, ``xbm`` and ``xpm``.

The ``area`` argument can be either of the following types:

-  ``String``: area is a CSS3 selector string, eg.
   ``div#plop form[name="form"] input[type="submit"]``
-  ``clipRect``: area is a clipRect object, eg.
   ``{"top":0,"left":0,"width":320,"height":200}``
-  ``Object``: area is a `selector object <selectors.html>`_, eg. an
   XPath selector

**Example:**

::

    casper.start('http://google.com', function() {
        // selector capture
        console.log(this.captureBase64('png', '#lga'));
        // clipRect capture
        console.log(this.captureBase64('png', {
            top: 0,
            left: 0,
            width: 320,
            height: 200
        }));
        // whole page capture
        console.log(this.captureBase64('png'));
    });

    casper.run();

.. raw:: html

   <h3 id="casper.captureSelector">

Casper#captureSelector(String targetFile, String selector)

.. raw:: html

   </h3>

Captures the page area containing the provided selector.

**Example:**

::

    casper.start('http://www.weather.com/', function() {
        this.captureSelector('weather.png', '#wx-main');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.clear">

Casper#clear()

.. raw:: html

   </h3>

Added in 0.6.5 Clears the current page execution environment context.
Useful to avoid having previously loaded DOM contents being still
active.

Think of it as a way to stop javascript execution within the remote DOM
environment.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.clear(); // javascript execution in this page has been stopped
    });

    casper.then(function() {
        // ...
    });

    casper.run();

.. raw:: html

   <h3 id="casper.debugHTML">

Casper#debugHTML([String selector, Boolean outer])

.. raw:: html

   </h3>

Outputs the results of ```getHTML()`` <#casper.getHTML>`_ directly to
the console. It takes the same arguments as ``getHTML()``.

.. raw:: html

   <h3 id="casper.debugPage">

Casper#debugPage()

.. raw:: html

   </h3>

Logs the textual contents of the current page directly to the standard
output, for debugging purpose.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.debugPage();
    });

    casper.run();

.. raw:: html

   <h3 id="casper.die">

Casper#die(String message[, int status])

.. raw:: html

   </h3>

Exits phantom with a logged error message and an optional exit status
code.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.die("Fail.", 1);
    });

    casper.run();

.. raw:: html

   <h3 id="casper.download">

Casper#download(String url, String target[, String method, Object data])

.. raw:: html

   </h3>

Saves a remote resource onto the filesystem. You can optionally set the
HTTP method using the ``method`` argument, and pass request arguments
through the ``data`` object (see
`base64encode <api.html#casper.base64encode>`_).

::

    casper.start('http://www.google.fr/', function() {
        var url = 'http://www.google.fr/intl/fr/about/corporate/company/';
        this.download(url, 'google_company.html');
    });

    casper.run(function() {
        this.echo('Done.').exit();
    });

.. raw:: html

   <h3 id="casper.each">

Casper#each(Array array, Function fn)

.. raw:: html

   </h3>

Iterates over provided array items and execute a callback.

**Example:**

::

    var links = [
        'http://google.com/',
        'http://yahoo.com/',
        'http://bing.com/'
    ];

    casper.start().each(links, function(self, link) {
        self.thenOpen(link, function() {
            this.echo(this.getTitle());
        });
    });

    casper.run();

Hint Have a look at the
`googlematch.js <https://github.com/n1k0/casperjs/blob/master/samples/googlematch.js>`_
sample script for a concrete use case.

.. raw:: html

   <h3 id="casper.echo">

Casper#echo(String message[, String style])

.. raw:: html

   </h3>

Prints something to stdout, optionally with some fancy color (see the
```Colorizer`` <#colorizer>`_ section of this document for more
information).

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.echo('Page title is: ' + this.evaluate(function() {
            return document.title;
        }), 'INFO'); // Will be printed in green on the console
    });

    casper.run();

.. raw:: html

   <h3 id="casper.evaluate">

Casper#evaluate(Function fn[, Object replacements])

.. raw:: html

   </h3>

Evaluates an expression **in the remote page context**, a bit like what
PhantomJS' ``WebPage#evaluate`` does, but can also handle passed
arguments if you define their context:

**Example:**

::

    casper.evaluate(function(username, password) {
        document.querySelector('#username').value = username;
        document.querySelector('#password').value = password;
        document.querySelector('#submit').click();
    }, {
        username: 'sheldon.cooper',
        password: 'b4z1ng4'
    });

Note For filling and submitting forms, rather use the
```Casper#fill()`` <#casper.fill>`_ method.

Note The concept behind this method is probably the most difficult to
understand when discovering CasperJS. As a reminder, think of the
``evaluate()`` method as a *gate* between the CasperJS environment and
the one of the page you have opened; everytime you pass a closure to
``evaluate()``, you're entering the page and execute code as if you were
using the browser console.

Here's a quickly drafted diagram trying to basically explain the
separation of concerns:

.. figure:: images/evaluate-diagram.png
   :align: center
   :alt: diagram

   diagram

.. raw:: html

   <h3 id="casper.evaluateOrDie">

Casper#evaluateOrDie(Function fn[, String message])

.. raw:: html

   </h3>

Evaluates an expression within the current page DOM and ``die()`` if it
returns anything but ``true``.

**Example:**

::

    casper.start('http://foo.bar/home', function() {
        this.evaluateOrDie(function() {
            return /logged in/.match(document.title);
        }, 'not authenticated');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.exit">

Casper#exit([int status])

.. raw:: html

   </h3>

Exits PhantomJS with an optional exit status code.

.. raw:: html

   <h3 id="casper.exists">

Casper#exists(String selector)

.. raw:: html

   </h3>

Checks if any element within remote DOM matches the provided
`selector <selectors.html>`_.

::

    casper.start('http://foo.bar/home', function() {
        if (this.exists('#my_super_id')) {
            this.echo('found #my_super_id', 'INFO');
        } else {
            this.echo('#my_super_id not found', 'ERROR');
        }
    });

    casper.run();

.. raw:: html

   <h3 id="casper.fetchText">

Casper#fetchText(String selector)

.. raw:: html

   </h3>

Retrieves text contents matching a given `selector
expression <selectors.html>`_. If you provide one matching more than one
element, their textual contents will be concatenated.

::

    casper.start('http://google.com/search?q=foo', function() {
        this.echo(this.fetchText('h3'));
    }).run();

.. raw:: html

   <h3 id="casper.forward">

Casper#forward()

.. raw:: html

   </h3>

Moves a step forward in browser's history.

::

    casper.start('http://foo.bar/1')
    casper.thenOpen('http://foo.bar/2');
    casper.thenOpen('http://foo.bar/3');
    casper.back();    // http://foo.bar/2
    casper.back();    // http://foo.bar/1
    casper.forward(); // http://foo.bar/2
    casper.run();

Also have a look at ```Casper.back()`` <#back>`_.

.. raw:: html

   <h3 id="casper.log">

Casper#log(String message[, String level, String space])

.. raw:: html

   </h3>

Logs a message with an optional level in an optional space. Available
levels are ``debug``, ``info``, ``warning`` and ``error``. A space is a
kind of namespace you can set for filtering your logs. By default,
Casper logs messages in two distinct spaces: ``phantom`` and ``remote``,
to distinguish what happens in the PhantomJS environment from the remote
one.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.log("I'm logging an error", "error");
    });

    casper.run();

.. raw:: html

   <h3 id="casper.fill">

Casper#fill(String selector, Object values[, Boolean submit])

.. raw:: html

   </h3>

Fills the fields of a form with given values and optionally submits it.

Example with this sample html form:

::

    <form action="/contact" id="contact-form" enctype="multipart/form-data">
        <input type="text" name="subject"/>
        <textearea name="content"></textearea>
        <input type="radio" name="civility" value="Mr"/> Mr
        <input type="radio" name="civility" value="Mrs"/> Mrs
        <input type="text" name="name"/>
        <input type="email" name="email"/>
        <input type="file" name="attachment"/>
        <input type="checkbox" name="cc"/> Receive a copy
        <input type="submit"/>
    </form>

A script to fill and submit this form:

::

    casper.start('http://some.tld/contact.form', function() {
        this.fill('form#contact-form', {
            'subject':    'I am watching you',
            'content':    'So be careful.',
            'civility':   'Mr',
            'name':       'Chuck Norris',
            'email':      'chuck@norris.com',
            'cc':         true,
            'attachment': '/Users/chuck/roundhousekick.doc'
        }, true);
    });

    casper.then(function() {
        this.evaluateOrDie(function() {
            return /message sent/.test(document.body.innerText);
        }, 'sending message failed');
    });

    casper.run(function() {
        this.echo('message sent').exit();
    });

Please Don't use CasperJS nor PhantomJS to send spam, or I'll be calling
the Chuck. More seriously, please just don't.

Warning The ``fill()`` method currently can't fill **file fields using
XPath selectors**; PhantomJS natively only allows the use of CSS3
selectors in its uploadFile method, hence this limitation.

.. raw:: html

   <h3 id="casper.getCurrentUrl">

Casper#getCurrentUrl()

.. raw:: html

   </h3>

Retrieves current page URL. Note the url will be url-decoded.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.echo(this.getCurrentUrl()); // "http://www.google.fr/"
    });

    casper.run();

.. raw:: html

   <h3 id="casper.getElementAttribute">

Casper#getElementAttribute(String selector, String attribute)

.. raw:: html

   </h3>

Added in 1.0 Retrieves the value of an attribute on the first element
matching the provided `selector <selectors.html>`_.

**Example:**

::

    var casper = require('casper').create();

    casper.start('http://www.google.fr/', function() {
        require('utils').dump(this.getElementAttribute('div[title="Google"]', 'title')); // "Google"
    });

    casper.run();

.. raw:: html

   <h3 id="casper.getElementBounds">

Casper#getElementBounds(String selector)

.. raw:: html

   </h3>

Retrieves boundaries for a DOM element matching the provided
`selector <selectors.html>`_.

It returns an Object with four keys: ``top``, ``left``, ``width`` and
``height``, or ``null`` if the selector doesn't exist.

**Example:**

::

    var casper = require('casper').create();

    casper.start('http://www.google.fr/', function() {
        require('utils').dump(this.getElementBounds('div[title="Google"]'));
    });

    casper.run();

This will output something like:

::

    {
        "height": 95,
        "left": 352,
        "top": 16,
        "width": 275
    }

.. raw:: html

   <h3 id="casper.getElementsBounds">

Casper#getElementsBounds(String selector)

.. raw:: html

   </h3>

Added in 1.0.0 Retrieves a list of boundaries for all DOM elements
matching the provided `selector <selectors.html>`_.

It returns an array of objects with four keys: ``top``, ``left``,
``width`` and ``height`` (see
`casper.getElementBounds() <#casper.getElementBounds>`_).

.. raw:: html

   <h3 id="casper.getElementInfo">

Casper#getElementInfo(String selector)

.. raw:: html

   </h3>

Retrieves information about the first element matching the provided
`selector <selectors.html>`_.

Added in 1.0
``js casper.start('http://google.com/', function() {     require('utils').dump(this.getElementInfo('#hplogo')); });``

Gives something like:

::

    {
        "nodeName": "div",
        "attributes": {
            "dir": "ltr",
            "title": "Google",
            "align": "left",
            "id": "hplogo",
            "onload": "window.lol&&lol()",
            "style": "background:url(images/srpr/logo3w.png) no-repeat;background-size:275px 95px;height:95px;width:275px"
        },
        "tag": "<div dir=\"ltr\" title=\"Google\" align=\"left\" id=\"hplogo\" onload=\"window.lol&amp;&amp;lol()\" style=\"background:url(images/srpr/logo3w.png) no-repeat;background-size:275px 95px;height:95px;width:275px\"><div nowrap=\"nowrap\" style=\"color:#777;font-size:16px;font-weight:bold;position:relative;left:214px;top:70px\">France</div></div>",
        "html": "<div nowrap=\"nowrap\" style=\"color:#777;font-size:16px;font-weight:bold;position:relative;left:214px;top:70px\">France</div>",
        "text": "France\n",
        "x": 582.5,
        "y": 192,
        "width": 275,
        "height": 95,
        "visible": true
    }

.. raw:: html

   <h3 id="casper.getFormValues">

Casper#getFormValues(String selector)

.. raw:: html

   </h3>

Added in 1.0 Retrieves a given form all of its field values.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.fill('form', {q: 'plop'}, false);
        this.echo(this.getFormValues('form').q); // 'plop'
    });

    casper.run();

.. raw:: html

   <h3 id="casper.getGlobal">

Casper#getGlobal(String name)

.. raw:: html

   </h3>

Retrieves a global variable value within the remote DOM environment by
its name. Basically, ``getGlobal('foo')`` will retrieve the value of
``window.foo`` from the page.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.echo(this.getGlobal('innerWidth')); // 1024
    });

    casper.run();

.. raw:: html

   <h3 id="casper.getHTML">

Casper#getHTML([String selector, Boolean outer])

.. raw:: html

   </h3>

Added in 1.0 Retrieves HTML code from the current page. By default, it
outputs the whole page HTML contents:

::

    casper.start('http://www.google.fr/', function() {
        this.echo(this.getHTML());
    });

    casper.run();

``getHTML()`` can also dump HTML contents matching a given `CSS3/XPath
selector <selectors.html>`_:

::

    <html>
      <body>
        <h1 id="foobar">Plop</h1>
      </body>
    </html>

::

    casper.start('http://www.site.tld/', function() {
        this.echo(this.getHTML('h1#foobar')); // => 'Plop'
    });

The ``outer`` argument allows to retrieve the outer HTML contents of the
matching element:

::

    casper.start('http://www.site.tld/', function() {
        this.echo(this.getHTML('h1#foobar', true)); // => '<h1 id="foobar">Plop</h1>'
    });

.. raw:: html

   <h3 id="casper.getPageContent">

Casper#getPageContent()

.. raw:: html

   </h3>

Added in 1.0.0 Retrieves current page contents, dealing with exotic
other content types than HTML.

**Example:**

::

    var casper = require('casper').create();

    casper.start().then(function() {
        this.open('http://search.twitter.com/search.json?q=casperjs', {
            method: 'get',
            headers: {
                'Accept': 'application/json'
            }
        });
    });

    casper.run(function() {
        require('utils').dump(JSON.parse(this.getPageContent()));
        this.exit();
    });

.. raw:: html

   <h3 id="casper.getTitle">

Casper#getTitle()

.. raw:: html

   </h3>

Retrieves current page title.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.echo(this.getTitle()); // "Google"
    });

    casper.run();

.. raw:: html

   <h3 id="casper.mouseEvent">

Casper#mouseEvent(String type, String selector)

.. raw:: html

   </h3>

Added in 0.6.9 Triggers a mouse event on the first element found
matching the provided selector.

Supported events are ``mouseup``, ``mousedown``, ``click``,
``mousemove``, ``mouseover`` and ``mouseout``.

**Example:**

::

    casper.start('http://www.google.fr/', function() {
        this.mouseEvent('click', 'h2 a');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.open">

Casper#open(String location, Object Settings)

.. raw:: html

   </h3>

Performs an HTTP request for opening a given location. You can forge
``GET``, ``POST``, ``PUT``, ``DELETE`` and ``HEAD`` requests.

**Example for a standard ``GET`` request:**

::

    casper.start();

    casper.open('http://www.google.com/').then(function() {
        this.echo('GOT it.');
    });

    casper.run();

**Example for a ``POST`` request:**

::

    casper.start();

    casper.open('http://some.testserver.com/post.php', {
        method: 'post',
        data:   {
            'title': 'Plop',
            'body':  'Wow.'
        }
    });

    casper.then(function() {
        this.echo('POSTED it.');
    });

    casper.run();

To pass nested parameters arrays:

::

    casper.open('http://some.testserver.com/post.php', {
           method: 'post',
           data: {
                'standard_param': 'foo',
                'nested_param[]': [       // please note the use of square brackets!
                    'Something',
                    'Something else'
                ]
           }
    });

Added in 1.0 You can also set custom request headers to send when
performing an outgoing request, passing the ``headers`` option:

::

    casper.open('http://some.testserver.com/post.php', {
        method: 'post',
        data:   {
            'title': 'Plop',
            'body':  'Wow.'
        },
        headers: {
            'Accept-Language': 'fr,fr-fr;q=0.8,en-us;q=0.5,en;q=0.3'
        }
    });

.. raw:: html

   <h3 id="casper.reload">

Casper#reload([Function then])

.. raw:: html

   </h3>

Added in 1.0 Reloads current page location.

**Example:**

::

    casper.start('http://google.com', function() {
        this.echo("loaded");
        this.reload(function() {
            this.echo("loaded again");
        });
    });

    casper.run();

.. raw:: html

   <h3 id="casper.repeat">

Casper#repeat(int times, function then)

.. raw:: html

   </h3>

Repeats a navigation step a given number of times.

**Example:**

::

    casper.start().repeat(3, function() {
        this.echo("Badger");
    });

    casper.run();

.. raw:: html

   <h3 id="casper.resourceExists">

Casper#resourceExists(Mixed test)

.. raw:: html

   </h3>

Checks if a resource has been loaded. You can pass either a function or
a string to perform the test.

**Example:**

::

    casper.start('http://www.google.com/', function() {
        if (this.resourceExists('logo3w.png')) {
            this.echo('Google logo loaded');
        } else {
            this.echo('Google logo not loaded', 'ERROR');
        }
    });

    casper.run();

Note If you want to wait for a resource to be loaded, use the
```waitForResource()`` <#casper.waitForResource>`_ method.

.. raw:: html

   <h3 id="casper.run">

Casper#run(fn onComplete[, int time])

.. raw:: html

   </h3>

Runs the whole suite of steps and optionally executes a callback when
they've all been done. Obviously, **calling this method is mandatory**
in order to run the Casper navigation suite.

Casper suite **won't run**:

::

    casper.start('http://foo.bar/home', function() {
        // ...
    });

    // hey, it's missing .run() here!

Casper suite **will run**:

::

    casper.start('http://foo.bar/home', function() {
        // ...
    });

    casper.run();

``Casper.run()`` also accepts an ``onComplete`` callback, which you can
consider as a custom final step to perform when all the other steps have
been executed. Just don't forget to ``exit()`` Casper if you define one!

::

    casper.start('http://foo.bar/home', function() {
        // ...
    });

    casper.then(function() {
        // ...
    });

    casper.run(function() {
        this.echo('So the whole suite ended.');
        this.exit(); // <--- don't forget me!
    });

.. raw:: html

   <h3 id="casper.sendKeys">

Casper#sendKeys(Selector selector, String keys[, Object options])

.. raw:: html

   </h3>

Added in 1.0 Sends native keyboard events to the element matching the
provided `selector <selectors.html>`_:

::

    casper.then(function() {
        this.sendKeys('form.contact input#name', 'Duke');
        this.sendKeys('form.contact textarea#message', "Damn, I'm looking good.");
        this.click('form.contact input[type="submit"]');
    });

.. raw:: html

   <h3 id="casper.setHttpAuth">

Casper#setHttpAuth(String username, String password)

.. raw:: html

   </h3>

Sets ``HTTP_AUTH_USER`` and ``HTTP_AUTH_PW`` values for HTTP based
authentication systems.

**Example:**

::

    casper.start();

    casper.setHttpAuth('sheldon.cooper', 'b4z1ng4');

    casper.thenOpen('http://password-protected.domain.tld/', function() {
        this.echo("I'm in. Bazinga.");
    })
    casper.run();

Of course you can directly pass the auth string in the url to open:

::

    var url = 'http://sheldon.cooper:b4z1ng4@password-protected.domain.tld/';

    casper.start(url, function() {
        this.echo("I'm in. Bazinga.");
    })

    casper.run();

.. raw:: html

   <h3 id="casper.start">

Casper#start(String url[, function then])

.. raw:: html

   </h3>

Configures and starts Casper, then open the provided ``url`` and
optionally adds the step provided by the ``then`` argument.

**Example:**

::

    casper.start('http://google.fr/', function() {
        this.echo("I'm loaded.");
    });

    casper.run();

Alternatively:

::

    casper.start('http://google.fr/');

    casper.then(function() {
        this.echo("I'm loaded.");
    });

    casper.run();

Or alternatively:

::

    casper.start('http://google.fr/');

    casper.then(function() {
        casper.echo("I'm loaded.");
    });

    casper.run();

Or even:

::

    casper.start('http://google.fr/');

    casper.then(function(self) {
        self.echo("I'm loaded.");
    });

    casper.run();

Matter of taste!

Note **You must call the ``start()`` method in order to be able to add
navigation steps** and run the suite. If you don't you'll get an error
message inviting you to do so anyway.

.. raw:: html

   <h3 id="casper.status">

Casper#status(Boolean asString)

.. raw:: html

   </h3>

Added in 1.0 Returns the status of current Casper instance.

**Example:**

::

    casper.start('http://google.fr/', function() {
        this.echo(this.status(true));
    });

    casper.run();

.. raw:: html

   <h3 id="casper.then">

Casper#then(Function fn)

.. raw:: html

   </h3>

This method is the standard way to add a new navigation step to the
stack, by providing a simple function:

::

    casper.start('http://google.fr/');

    casper.then(function() {
        this.echo("I'm in your google.");
    });

    casper.then(function() {
        this.echo('Now, let me write something');
    });

    casper.then(function() {
        this.echo('Oh well.');
    });

    casper.run();

You can add as many steps as you need. Note that the current ``Casper``
instance automatically binds the ``this`` keyword for you within step
functions.

To run all the steps you defined, call the ```run()`` <#run>`_ method,
and voila.

Note You must ```start()`` <#start>`_ the casper instance in order to
use the ``then()`` method.

.. raw:: html

   <h4 id="casper.then.callbacks">

Accessing the current HTTP response

.. raw:: html

   </h4>

Added in 1.0 You can access the current HTTP response object using the
first parameter of your step callback:

::

    casper.start('http://www.google.fr/', function(response) {
        require('utils').dump(response);
    });

That gives:

::

    $ casperjs dump-headers.js
    {
        "contentType": "text/html; charset=UTF-8",
        "headers": [
            {
                "name": "Date",
                "value": "Thu, 18 Oct 2012 08:17:29 GMT"
            },
            {
                "name": "Expires",
                "value": "-1"
            },
            // ... lots of other headers
        ],
        "id": 1,
        "redirectURL": null,
        "stage": "end",
        "status": 200,
        "statusText": "OK",
        "time": "2012-10-18T08:17:37.068Z",
        "url": "http://www.google.fr/"
    }

So to fetch a particular header by its name:

::

    casper.start('http://www.google.fr/', function(response) {
        this.echo(response.headers.get('Date'));
    });

That gives:

::

    $ casperjs dump-headers.js
    Thu, 18 Oct 2012 08:26:34 GMT

.. raw:: html

   <h3 id="casper.thenClick">

Casper#thenClick(String selector)

.. raw:: html

   </h3>

Adds a new navigation step to click a given selector and add a new
navigation step in a single operation.

**Example:**

::

    // Querying for "Chuck Norris" on Google
    casper.start('http://casperjs.org/').thenClick('a', function() {
        this.echo("I clicked on first link found, the page is now loaded.");
    });

    casper.run();

This method is basically a convenient a shortcut for chaining a
```then()`` <#then>`_ and an ```evaluate()`` <#evaluate>`_ calls.

.. raw:: html

   <h3 id="casper.thenEvaluate">

Casper#thenEvaluate(Function fn[, Object replacements])

.. raw:: html

   </h3>

Adds a new navigation step to perform code evaluation within the current
retrieved page DOM.

**Example:**

::

    // Querying for "Chuck Norris" on Google
    casper.start('http://google.fr/').thenEvaluate(function(term) {
        document.querySelector('input[name="q"]').setAttribute('value', term);
        document.querySelector('form[name="f"]').submit();
    }, {
        term: 'Chuck Norris'
    });

    casper.run();

This method is basically a convenient a shortcut for chaining a
```then()`` <#then>`_ and an ```evaluate()`` <#evaluate>`_ calls.

.. raw:: html

   <h3 id="casper.thenOpen">

Casper#thenOpen(String location[, mixed options])

.. raw:: html

   </h3>

Adds a new navigation step for opening a new location, and optionally
add a next step when its loaded.

**Example:**

::

    casper.start('http://google.fr/').then(function() {
        this.echo("I'm in your google.");
    });

    casper.thenOpen('http://yahoo.fr/', function() {
        this.echo("Now I'm in your yahoo.")
    });

    casper.run();

Added in 1.0 You can also specify request settings by passing a `setting
object <#casper.open>`_ as the second argument:

::

    casper.start().thenOpen('http://url.to/some/uri', {
        method: "post",
        data: {
          username: 'chuck',
          password: 'n0rr15'
        }
    }, function() {
        this.echo("POST request has been sent.")
    });

    casper.run();

.. raw:: html

   <h3 id="casper.thenOpenAndEvaluate">

Casper#thenOpenAndEvaluate(String location[, function then, Object
replacements])

.. raw:: html

   </h3>

Basically a shortcut for opening an url and evaluate code against remote
DOM environment.

**Example:**

::

    casper.start('http://google.fr/').then(function() {
        this.echo("I'm in your google.");
    });

    casper.thenOpenAndEvaluate('http://yahoo.fr/', function() {
        var f = document.querySelector('form');
        f.querySelector('input[name=q]').value = 'chuck norris';
        f.submit();
    });

    casper.run(function() {
        this.debugPage();
        this.exit();
    });

.. raw:: html

   <h3 id="casper.toString">

Casper#toString()

.. raw:: html

   </h3>

Added in 1.0 Returns a string representation of current Casper instance.

**Example:**

::

    casper.start('http://google.fr/', function() {
        this.echo(this); // [object Casper], currently at http://google.fr/
    });

    casper.run();

.. raw:: html

   <h3 id="casper.userAgent">

Casper#userAgent(String agent)

.. raw:: html

   </h3>

Added in 1.0 Sets the `User-Agent
string <http://en.wikipedia.org/wiki/User-Agent>`_ to send through
headers when performing requests.

**Example:**

::

    casper.start();

    casper.userAgent('Mozilla/5.0 (Macintosh; Intel Mac OS X)');

    casper.thenOpen('http://google.com/', function() {
        this.echo("I'm a Mac.");
    });

    casper.userAgent('Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)');

    casper.thenOpen('http://google.com/', function() {
        this.echo("I'm a PC.");
    });

    casper.run();

.. raw:: html

   <h3 id="casper.viewport">

Casper#viewport(Number width, Number height)

.. raw:: html

   </h3>

Changes current viewport size.

**Example:**

::

    casper.viewport(1024, 768);

Note PhantomJS comes with a default viewport size of 400x300, and
CasperJS doesn't override it by default.

.. raw:: html

   <h3 id="casper.visible">

Casper#visible(String selector)

.. raw:: html

   </h3>

Checks if the DOM element matching the provided `selector
expression <selectors.html>`_ is visible in remote page.

**Example:**

::

    casper.start('http://google.com/', function() {
        if (this.visible('#hplogo')) {
            this.echo("I can see the logo");
        } else {
            this.echo("I can't see the logo");
        }
    });

.. raw:: html

   <h3 id="casper.wait">

Casper#wait(Number timeout[, Function then])

.. raw:: html

   </h3>

Pause steps suite execution for a given amount of time, and optionally
execute a step on done.

**Example:**

::

    casper.start('http://yoursite.tld/', function() {
        this.wait(1000, function() {
            this.echo("I've waited for a second.");
        });
    });

    casper.run();

You can also write the same thing like this:

::

    casper.start('http://yoursite.tld/');

    casper.wait(1000, function() {
        this.echo("I've waited for a second.");
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitFor">

Casper#waitFor(Function testFx[, Function then, Function onTimeout,
Number timeout])

.. raw:: html

   </h3>

Waits until a function returns true to process any next step.

You can also set a callback on timeout using the ``onTimeout`` argument,
and set the timeout using the ``timeout`` one, in milliseconds. The
default timeout is set to 5000ms.

**Example:**

::

    casper.start('http://yoursite.tld/');

    casper.waitFor(function check() {
        return this.evaluate(function() {
            return document.querySelectorAll('ul.your-list li').length > 2;
        });
    }, function then() {
        this.captureSelector('yoursitelist.png', 'ul.your-list');
    });

    casper.run();

Example using the ``onTimeout`` callback:

::

    casper.start('http://yoursite.tld/');

    casper.waitFor(function check() {
        return this.evaluate(function() {
            return document.querySelectorAll('ul.your-list li').length > 2;
        });
    }, function then() {    // step to execute when check() is ok
        this.captureSelector('yoursitelist.png', 'ul.your-list');
    }, function timeout() { // step to execute if check has failed
        this.echo("I can't haz my screenshot.").exit();
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitForPopup">

Casper#waitForPopup(String\|RegExp urlPattern[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Added in 1.0 Waits for a popup having its url matching the provided
pattern to be opened and loaded.

The currently loaded popups are available in the ``Casper.popups``
array-like property.

::

    casper.start('http://foo.bar/').then(function() {
        this.test.assertTitle('Main page title');
        this.clickLabel('Open me a popup');
    });

    // this will wait for the popup to be opened and loaded
    casper.waitForPopup(/popup\.html$/, function() {
        this.test.assertEquals(this.popups.length, 1);
    });

    // this will set the popup DOM as the main active one only for time the
    // step closure being executed
    casper.withPopup(/popup\.html$/, function() {
        this.test.assertTitle('Popup title');
    });

    // next step will automatically revert the current page to the initial one
    casper.then(function() {
        this.test.assertTitle('Main page title');
    });

.. raw:: html

   <h3 id="casper.waitForSelector">

Casper#waitForSelector(String selector[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Waits until an element matching the provided `selector
expression <selectors.html>`_ exists in remote DOM to process any next
step. Uses `Casper.waitFor() <#casper.waitFor>`_.

**Example:**

::

    casper.start('https://twitter.com/#!/n1k0');

    casper.waitForSelector('.tweet-row', function() {
        this.captureSelector('twitter.png', 'html');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitWhileSelector">

Casper#waitWhileSelector(String selector[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Waits until an element matching the provided `selector
expression <selectors.html>`_ does not exist in remote DOM to process a
next step. Uses `Casper.waitFor() <#casper.waitFor>`_.

**Example:**

::

    casper.start('http://foo.bar/');

    casper.waitWhileSelector('.selector', function() {
        this.echo('.selector is no more!');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitForResource">

Casper#waitForResource(Function testFx[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Wait until a resource that matches the given ``testFx`` is loaded to
process a next step. Uses `Casper.waitFor() <#casper.waitFor>`_.

**Example:**

::

    casper.start('http://foo.bar/', function() {
        this.waitForResource("foobar.png");
    });

    casper.then(function() {
        this.echo('foobar.png has been loaded.');
    });

    casper.run();

Another way to write the exact same behavior:

::

    casper.start('http://foo.bar/');

    casper.waitForResource("foobar.png", function() {
        this.echo('foobar.png has been loaded.');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitForText">

Casper#waitForText(String text[, Function then, Function onTimeout,
Number timeout])

.. raw:: html

   </h3>

Added in 1.0 Waits until the passed text is present in the page contents
before processing the immediate next step. Uses
`Casper.waitFor() <#casper.waitFor>`_.

**Example:**

::

    casper.start('http://why.univer.se/').waitForText("42", function() {
        this.echo('Found the answer.');
    });

    casper.run();

.. raw:: html

   <h3 id="casper.waitUntilVisible">

Casper#waitUntilVisible(String selector[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Waits until an element matching the provided `selector
expression <selectors.html>`_ is visible in the remote DOM to process a
next step. Uses `Casper.waitFor() <#casper.waitFor>`_.

.. raw:: html

   <h3 id="casper.waitWhileVisible">

Casper#waitWhileVisible(String selector[, Function then, Function
onTimeout, Number timeout])

.. raw:: html

   </h3>

Waits until an element matching the provided `selector
expression <selectors.html>`_ is no longer visible in remote DOM to
process a next step. Uses `Casper.waitFor() <#casper.waitFor>`_.

.. raw:: html

   <h3 id="casper.warn">

Casper#warn(String message)

.. raw:: html

   </h3>

Logs and prints a warning message to the standard output.

::

    casper.warn("I'm a warning message.");

.. raw:: html

   <h3 id="casper.withFrame">

Casper#withFrame(String\|Number frameInfo, Function then)

.. raw:: html

   </h3>

Added in 1.0 Switches the main page to the frame having the name or
frame index number matching the passed argument, and processes a step.
The page context switch only lasts until the step execution is finished:

::

    casper.start('tests/site/frames.html', function() {
        this.test.assertTitle('FRAMESET TITLE');
    });

    casper.withFrame('frame1', function() {
        this.test.assertTitle('FRAME TITLE');
    });

    casper.withFrame(0, function() {
        this.test.assertTitle('FRAME TITLE');
    });

    casper.then(function() {
        this.test.assertTitle('FRAMESET TITLE');
    });

.. raw:: html

   <h3 id="casper.withPopup">

Casper#withPopup(Mixed popupInfo, Function step)

.. raw:: html

   </h3>

Added in 1.0 Switches the main page to a popup matching the information
passed as argument, and processes a step. The page context switch only
lasts until the step execution is finished:

::

    casper.start('http://foo.bar/').then(function() {
        this.test.assertTitle('Main page title');
        this.clickLabel('Open me a popup');
    });

    // this will wait for the popup to be opened and loaded
    casper.waitForPopup(/popup\.html$/, function() {
        this.test.assertEquals(this.popups.length, 1);
    });

    // this will set the popup DOM as the main active one only for time the
    // step closure being executed
    casper.withPopup(/popup\.html$/, function() {
        this.test.assertTitle('Popup title');
    });

    // next step will automatically revert the current page to the initial one
    casper.then(function() {
        this.test.assertTitle('Main page title');
    });

**Note:** The currently loaded popups are available in the
``Casper.popups`` array-like property.

.. raw:: html

   <h3 id="casper.zoom">

Casper#zoom(Number factor)

.. raw:: html

   </h3>

Added in 1.0 Sets the current page zoom factor.

::

    var casper = require('casper').create();

    casper.start().zoom(2).thenOpen('http://google.com', function() {
        this.capture('big-google.png');
    });

    casper.run();

