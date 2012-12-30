=====================
The ``events`` module
=====================

CasperJS provides an `event handler <#events>`_ very similar to the
`one <https://github.com/joyent/node/blob/master/lib/events.js>`_
shipping with `nodejs <http://nodejs.org>`_; actually it borrows most of
its codebase. CasperJS also adds `*filters* <#filters>`_, which are
basically ways to alter values asynchronously.

--------------

.. raw:: html

   <h2 id="events">

Events

.. raw:: html

   </h2>

Using events is pretty much straightforward if you're a node developer,
or if you worked with any evented system before:

::

    var casper = require('casper').create();

    casper.on('resource.received', function(resource) {
        casper.echo(resource.url);
    });

Here's a table containing all the available events with all the
parameters passed to their callback:

.. raw:: html

   <table class="table table-striped table-condensed" caption="Casper events">
     <thead>
       <tr>
         <th>

Name

.. raw:: html

   </th>
         <th>

Arguments

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

back

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when the embedded browser is asked to go back a step in its
history.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

capture.saved

.. raw:: html

   </td>
         <td>

targetFile

.. raw:: html

   </td>
         <td>

Emitted when a screenshot image has been captured.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

click

.. raw:: html

   </td>
         <td>

selector

.. raw:: html

   </td>
         <td>

Emitted when the Casper.click() method has been called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

die

.. raw:: html

   </td>
         <td>

message, status

.. raw:: html

   </td>
         <td>

Emitted when the Casper.die() method has been called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

downloaded.file

.. raw:: html

   </td>
         <td>

targetPath

.. raw:: html

   </td>
         <td>

Emitted when a file has been downloaded by Casper.download(); target
will contain the path to the downloaded file.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

error

.. raw:: html

   </td>
         <td>

msg, backtrace

.. raw:: html

   </td>
         <td>


Added in 0.6.9 Emitted when an error hasn't been caught. Do basically
what PhantomJS' onError() native handler does.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

exit

.. raw:: html

   </td>
         <td>

status

.. raw:: html

   </td>
         <td>

Emitted when the Casper.exit() method has been called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

fill

.. raw:: html

   </td>
         <td>

selector, vals, submit

.. raw:: html

   </td>
         <td>

Emitted when a form is filled using the Casper.fill() method.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

forward

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when the embedded browser is asked to go forward a step in its
history.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

http.auth

.. raw:: html

   </td>
         <td>

username, password

.. raw:: html

   </td>
         <td>

Emitted when http authentication parameters are set.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

http.status.[code]

.. raw:: html

   </td>
         <td>

resource

.. raw:: html

   </td>
         <td>
           <p>


Emitted when any given HTTP reponse is received with the status code
specified by [code], eg.:

.. raw:: html

   </p>
           <pre class="prettyprint">casper.on('http.status.404', function(resource) {
       casper.echo(resource.url + ' is 404');
   })</pre>
           </td>
       </td>
       <tr>
         <td>

load.started

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when PhantomJS' WebPage.onLoadStarted event callback is called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

load.failed

.. raw:: html

   </td>
         <td>

Object

.. raw:: html

   </td>
         <td>


Emitted when PhantomJS' WebPage.onLoadFinished event callback has been
called and failed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

load.finished

.. raw:: html

   </td>
         <td>

status

.. raw:: html

   </td>
         <td>

Emitted when PhantomJS' WebPage.onLoadFinished event callback is called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

log

.. raw:: html

   </td>
         <td>

entry

.. raw:: html

   </td>
         <td>
           <p>

Emitted when the Casper.log() method has been called. The entry
parameter is an Object like this:

.. raw:: html

   </p>
           <pre class="prettyprint">{
       level:   "debug",
       space:   "phantom",
       message: "A message",
       date:    "a javascript Date instance"
   }</pre>
         </td>
       </tr>
       <tr>
         <td>

mouse.click

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

Emitted when the mouse left-click something or somewhere.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

mouse.down

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

Emitted when the mouse presses on something or somewhere with the left
button.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

mouse.move

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

Emitted when the mouse moves onto something or somewhere.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

mouse.up

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

Emitted when the mouse releases the left button over something or
somewhere.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

navigation.requested

.. raw:: html

   </td>
         <td>

url, navigationType, navigationLocked, isMainFrame

.. raw:: html

   </td>
         <td>
           <p>


Added in 1.0 Emitted each time a navigation operation has been
requested. Available navigation types are: ``LinkClicked``,
``FormSubmitted``, ``BackOrForward``, ``Reload``, ``FormResubmitted``
and ``Other``.

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

open

.. raw:: html

   </td>
         <td>

location, settings

.. raw:: html

   </td>
         <td>
           <p>

Emitted when an HTTP request is sent. First callback arg is the
location, second one is a request settings Object of the form:

.. raw:: html

   </p>
           <pre class="prettyprint">{
       method: "post",
       data:   "foo=42&amp;chuck=norris"
   }</pre>
         </td>
       </tr>
       <tr>
         <td>

page.created

.. raw:: html

   </td>
         <td>

page

.. raw:: html

   </td>
         <td>

Emitted when PhantomJS' WebPage object used by CasperJS has been
created.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

page.error

.. raw:: html

   </td>
         <td>

message, trace

.. raw:: html

   </td>
         <td>


Emitted when retrieved page leaved a Javascript error uncaught:

.. raw:: html

   <pre class="prettyprint">casper.on("page.error", function(msg, trace) {
       this.echo("Error: " + msg, "ERROR");
   });</pre>
         </td>
       </tr>
       <tr>
         <td>

page.initialized

.. raw:: html

   </td>
         <td>

page

.. raw:: html

   </td>
         <td>

Emitted when PhantomJS' WebPage object used by CasperJS has been
initialized.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

page.resource.received

.. raw:: html

   </td>
         <td>

response

.. raw:: html

   </td>
         <td>

Emitted when the HTTP response corresponding to current required url has
been received.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

page.resource.requested

.. raw:: html

   </td>
         <td>

request

.. raw:: html

   </td>
         <td>

Emitted when a new HTTP request is performed to open the required url.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

popup.created

.. raw:: html

   </td>
         <td>

WebPage

.. raw:: html

   </td>
         <td>

Emitted when a new window has been opened.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

popup.loaded

.. raw:: html

   </td>
         <td>

WebPage

.. raw:: html

   </td>
         <td>

Emitted when a new window has been loaded.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

popup.closed

.. raw:: html

   </td>
         <td>

WebPage

.. raw:: html

   </td>
         <td>

Emitted when a new opened window has been closed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

popup.created

.. raw:: html

   </td>
         <td>

WebPage

.. raw:: html

   </td>
         <td>

Emitted when a new window has been opened.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

remote.alert

.. raw:: html

   </td>
         <td>

message

.. raw:: html

   </td>
         <td>

Emitted when a remote alert() call has been performed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

remote.message

.. raw:: html

   </td>
         <td>

msg

.. raw:: html

   </td>
         <td>

Emitted when any remote console logging call has been performed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

resource.received

.. raw:: html

   </td>
         <td>

resource

.. raw:: html

   </td>
         <td>

Emitted when any resource has been received.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

resource.requested

.. raw:: html

   </td>
         <td>

request

.. raw:: html

   </td>
         <td>

Emitted when any resource has been requested.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

run.complete

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when the whole series of steps in the stack have been executed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

run.start

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when Casper.run() is called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

starting

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when Casper.start() is called.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

started

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when Casper has been started using Casper.start().

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

step.added

.. raw:: html

   </td>
         <td>

step

.. raw:: html

   </td>
         <td>

Emitted when a new navigation step has been added to the stack.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

step.complete

.. raw:: html

   </td>
         <td>

stepResult

.. raw:: html

   </td>
         <td>

Emitted when a navigation step has been executed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

step.created

.. raw:: html

   </td>
         <td>

fn

.. raw:: html

   </td>
         <td>

Emitted when a new navigation step has been created.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

step.start

.. raw:: html

   </td>
         <td>

step

.. raw:: html

   </td>
         <td>

Emitted when a navigation step has been started.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

step.timeout

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when a navigation step has been executed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

timeout

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>


Emitted when the execution time of the script has reached the
Casper.options.timeout value.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

url.changed

.. raw:: html

   </td>
         <td>

url

.. raw:: html

   </td>
         <td>
           <p>


Added in 1.0 Emitted each time the current page url changes.

.. raw:: html

   </p>
         </td>
       </tr>
       <tr>
         <td>

viewport.changed

.. raw:: html

   </td>
         <td>

[width, height]

.. raw:: html

   </td>
         <td>

Emitted when the viewport has been changed.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

wait.done

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when a Casper.wait\*() operation ends.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

wait.start

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>

Emitted when a Casper.wait\*() operation starts.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

waitFor.timeout

.. raw:: html

   </td>
         <td>

None

.. raw:: html

   </td>
         <td>


Emitted when the execution time of a Casper.wait\*() operation has
exceeded the value of Casper.options.stepTimeout.

.. raw:: html

   </td>
       </tr>
     </tbody>
   </table>

Emitting you own events
~~~~~~~~~~~~~~~~~~~~~~~

Of course you can emit your own events, using the ``Casper.emit()``
method:

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

--------------

.. raw:: html

   <h2 id="filters">

Filters

.. raw:: html

   </h2>

Filters allow you to alter some values asynchronously. Sounds obscure?
Let's take a simple example and imagine you would like to alter every
single url opened by CasperJS to append a ``foo=42`` query string
parameter:

::

    var casper = require('casper').create();

    casper.setFilter('open.location', function(location) {
        return /\?+/.test(location) ? location += "&foo=42" : location += "?foo=42";
    });

There you have it, every single requested url will have this appended.
Let me bet you'll find far more interesting use cases than my silly one
;)

Here'a the list of all available filters with their expected return
value:

.. raw:: html

   <table class="table table-striped table-condensed" caption="Casper options">
     <thead>
       <tr>
         <th>

Name

.. raw:: html

   </th>
         <th>

Arguments

.. raw:: html

   </th>
         <th>

Return type

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

capture.target\_filename

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>

Allows to alter the value of the filename where a screen capture should
be stored.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

echo.message

.. raw:: html

   </td>
         <td>

message

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>

Allows to alter every message written onto stdout.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

log.message

.. raw:: html

   </td>
         <td>

message

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>

Allows to alter every log message.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

open.location

.. raw:: html

   </td>
         <td>

args

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>

Allows to alter every url before it being opened.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td>

page.confirm

.. raw:: html

   </td>
         <td>

message

.. raw:: html

   </td>
         <td>

Boolean

.. raw:: html

   </td>
         <td>
           <p>


Added in 1.0 Allows to react on a javascript confirm() call:

.. raw:: html

   </p>
           <pre class="prettyprint">casper.setFilter("page.confirm", function(msg) {
       return msg === "Do you like vbscript?" ? false : true;
   });</pre>
         </td>
       <tr>
         <td>

page.prompt

.. raw:: html

   </td>
         <td>

message, value

.. raw:: html

   </td>
         <td>

String

.. raw:: html

   </td>
         <td>
           <p>


Added in 1.0 Allows to react on a javascript prompt() call:

.. raw:: html

   </p>
           <pre class="prettyprint">casper.setFilter("page.prompt", function(msg, value) {
       if (msg === "What's your name?") {
           return "Chuck";
       }
   });</pre>
         </td>
       </tr>
     </tbody>
   </table>


