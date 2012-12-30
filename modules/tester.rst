=====================
The ``tester`` module
=====================

Casper ships with a ``tester`` module and a ``Tester`` class providing
an API for unit & functional testing purpose. By default you can access
an instance of this class through the ``test`` property of any
``Casper`` class instance.

Note The best way to learn how to use the Tester API and see it in
action is probably to have a look at the `CasperJS test suite
code <https://github.com/n1k0/casperjs/blob/master/tests/run.js>`_.

.. raw:: html

   <h3 id="tester.assert">

Tester#assert(Boolean condition[, String message])

.. raw:: html

   </h3>

Asserts that the provided condition strictly resolves to a boolean
``true``.

::

    var url = 'http://www.google.fr/';
    var casper = require('casper').create();
    casper.start(url, function() {
        this.test.assert(this.getCurrentUrl() === url, 'url is the one expected');
    });

.. raw:: html

   <h3 id="tester.assertDoesntExist">

Tester#assertDoesntExist(String selector[, String message])

.. raw:: html

   </h3>

Asserts that an element matching the provided `selector
expression <selectors.html>`_ doesn't exists within the remote DOM
environment.

::

    var casper = require('casper').create();
    casper.start('http://www.google.fr/', function() {
        this.test.assertDoesntExist('form[name="gs"]', 'google.fr has a form with name "gs"');
    });

.. raw:: html

   <h3 id="tester.assertEquals">

Tester#assertEquals(mixed testValue, mixed expected[, String message])

.. raw:: html

   </h3>

Asserts that two values are strictly equals.

::

    var url = 'http://www.google.fr/';
    var casper = require('casper').create();
    casper.start(url, function() {
        this.test.assertEquals(this.getCurrentUrl(), url, 'url is the one expected');
    });

.. raw:: html

   <h3 id="tester.assertEval">

Tester#assertEval(Function fn[, String message, Mixed arguments])

.. raw:: html

   </h3>

Asserts that a `code evaluation in remote
DOM <api.html#casper.evaluate>`_ strictly resolves to a boolean
``true``.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertEval(function() {
            return document.querySelectorAll('form').length > 0;
        }, 'google.fr has at least one form');
        this.test.assertEval(function(title) {
            return document.title === title;
        }, 'google.fr title is "Google"', 'Google');
    });

.. raw:: html

   <h3 id="tester.assertEvalEquals">

Tester#assertEvalEquals(Function fn, mixed expected[, String message,
Mixed arguments])

.. raw:: html

   </h3>

Asserts that the result of a `code evaluation in remote
DOM <api.html#casper.evaluate>`_ strictly equals to the expected value.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertEvalEquals(function() {
            return document.querySelectorAll('form').length;
        }, 1, 'google.fr provides a single form tag');
        this.test.assertEval(function(title) {
            return document.title;
        }, 'Google', 'google.fr title is "Google"');
    });

.. raw:: html

   <h3 id="tester.assertExists">

Tester#assertExists(String selector[, String message])

.. raw:: html

   </h3>

Asserts that an element matching the provided `selector
expression <selectors.html>`_ exists in remote DOM environment.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertExists('form[name="gs"]', 'google.fr has a form with name "gs"');
    });

.. raw:: html

   <h3 id="tester.assertFalsy">

Tester#assertFalsy(Mixed subject[, String message])

.. raw:: html

   </h3>

Added in 1.0 Asserts that a given subject is
`falsy <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. raw:: html

   <h3 id="tester.assertField">

Tester#assertField(String inputName, String expected[, String message])

.. raw:: html

   </h3>

Asserts that a given form field has the provided value:

::

    casper.start('http://www.google.fr/', function() {
        this.fill('form[name="gs"]', { q: 'plop' }, false);
        this.test.assertField('q', 'plop');
    });

Added in 1.0.0 This also works with any input type: ``select``,
``textarea``, etc.

.. raw:: html

   <h3 id="tester.assertHttpStatus">

Tester#assertHttpStatus(Number status[, String message])

.. raw:: html

   </h3>

Asserts that current `HTTP status
code <http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html>`_ is the
same as the one passed as argument.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertHttpStatus(200, 'google.fr is up');
    });

.. raw:: html

   <h3 id="tester.assertMatch">

Tester#assertMatch(mixed subject, RegExp pattern[, String message])

.. raw:: html

   </h3>

Asserts that a provided string matches a provided javascript ``RegExp``
pattern.

::

    casper.test.assertMatch('Chuck Norris', /^chuck/i, 'Chuck Norris' first name is Chuck');

.. raw:: html

   <h3 id="tester.assertNot">

Tester#assertNot(mixed subject[, String message])

.. raw:: html

   </h3>

Asserts that the passed subject resolves to some `falsy
value <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

::

    casper.test.assertNot(false, "Universe is still operational");

.. raw:: html

   <h3 id="tester.assertNotEquals">

Tester#assertNotEquals(mixed testValue, mixed expected[, String
message])

.. raw:: html

   </h3>

Added in 0.6.7 Asserts that two values are **not** strictly equals.

::

    casper.test.assertNotEquals(true, "Truth is out");

.. raw:: html

   <h3 id="tester.assertNotVisible">

Tester#assertNotVisible(String selector[, String message])

.. raw:: html

   </h3>

Asserts that the element matching the provided `selector
expression <selectors.html>`_ is not visible.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertNotVisible('h6');
    });

.. raw:: html

   <h3 id="tester.assertRaises">

Tester#assertRaises(Function fn, Array args[, String message])

.. raw:: html

   </h3>

Asserts that the provided function called with the given parameters
raises a javascript ``Error``.

::

    casper.test.assertRaises(function(throwIt) {
        if (throwIt) {
            throw new Error('thrown');
        }
    }, [true], 'Error has been raised.');

    casper.test.assertRaises(function(throwIt) {
        if (throwIt) {
            throw new Error('thrown');
        }
    }, [false], 'Error has been raised.'); // fails

.. raw:: html

   <h3 id="tester.assertSelectorDoesntHaveText">

Tester#assertSelectorDoesntHaveText(String selector, String text[,
String message])

.. raw:: html

   </h3>

Asserts that given text does not exist in the provided
`selector <selectors.html>`_.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorDoesntHaveText('title', 'Yahoo!');
    });

.. raw:: html

   <h3 id="tester.assertSelectorExists">

Tester#assertSelectorExists(String selector[, String message])

.. raw:: html

   </h3>

Asserts that at least an element matching the provided `selector
expression <selectors.html>`_ exists in remote DOM.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorExists('form[name="gs"]', 'google.fr provides a form');
    });

.. raw:: html

   <h3 id="tester.assertSelectorHasText">

Tester#assertSelectorHasText(String selector, String text[, String
message])

.. raw:: html

   </h3>

Asserts that given text exists in the provided
`selector <selectors.html>`_.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorHasText('title', 'Google');
    });

.. raw:: html

   <h3 id="tester.assertResourceExists">

Tester#assertResourceExists(Function testFx[, String message])

.. raw:: html

   </h3>

The ``testFx`` function is executed against all loaded assets and the
test passes when at least one resource matches.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertResourceExists(function (resource) {
          return resource.url.match('logo3w.png');
        }, 'google.fr logo was loaded');
        // or shorter
        this.test.assertResourceExists('logo3w.png', 'google.fr logo was loaded');
    });

Check the documentation for
```Casper.resourceExists()`` <api.html#casper.resourceExists>`_.

.. raw:: html

   <h3 id="tester.assertTextExists">

Tester#assertTextExists(String expected[, String message])

.. raw:: html

   </h3>

Asserts that body **plain text content** contains the given string.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTextExists('google', 'page body contains "google"');
    });

.. raw:: html

   <h3 id="tester.assertTextDoesntExist">

Tester#assertTextDoesntExist(String unexpected[, String message])

.. raw:: html

   </h3>

Added in 1.0 Asserts that body **plain text content** doesn't contain
the given string.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTextDoesntExist('bing', 'page body does not contain "bing"');
    });

.. raw:: html

   <h3 id="tester.assertTitle">

Tester#assertTitle(String expected[, String message])

.. raw:: html

   </h3>

Asserts that title of the remote page equals to the expected one.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTitle('Google', 'google.fr has the correct title');
    });

.. raw:: html

   <h3 id="tester.assertTitleMatch">

Tester#assertTitleMatch(RegExp pattern[, String message])

.. raw:: html

   </h3>

Asserts that title of the remote page matches the provided RegExp
pattern.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTitleMatch(/Google/, 'google.fr has a quite predictable title');
    });

.. raw:: html

   <h3 id="tester.assertTruthy">

Tester#assertTruthy(Mixed subject[, String message])

.. raw:: html

   </h3>

Added in 1.0 Asserts that a given subject is
`truthy <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. raw:: html

   <h3 id="tester.assertType">

Tester#assertType(mixed input, String type[, String message])

.. raw:: html

   </h3>

Asserts that the provided input is of the given type.

::

    casper.test.assertType(42, "number", "Okay, 42 is a number");
    casper.test.assertType([1, 2, 3], "array", "Yeah, we can test for arrays too =)");

.. raw:: html

   <h3 id="tester.assertUrlMatch">

Tester#assertUrlMatch(Regexp pattern[, String message])

.. raw:: html

   </h3>

Asserts that a the current page url matches the provided RegExp pattern.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertUrlMatch(/^http:\/\//', 'google.fr is served in http://');
    });

.. raw:: html

   <h3 id="tester.assertVisible">

Tester#assertVisible(String selector[, String message])

.. raw:: html

   </h3>

Asserts that the element matching the provided `selector
expression <selectors.html>`_ is visible.

::

    casper.start('http://www.google.fr/', function() {
        this.test.assertVisible('h1');
    });

.. raw:: html

   <h3 id="tester.colorize">

Tester#colorize(String message, String style)

.. raw:: html

   </h3>

Render a colorized output. Basically a proxy method for
``Casper.Colorizer#colorize()``.

.. raw:: html

   <h3 id="tester.comment">

Tester#comment(String message)

.. raw:: html

   </h3>

Writes a comment-style formatted message to stdout.

::

    casper.test.comment("Hi, I'm a comment");

.. raw:: html

   <h3 id="tester.done">

Tester#done([Number expected])

.. raw:: html

   </h3>

Flag a test file execution as being finished:

::

    casper.test.assert(true);
    casper.test.assertNot(false);
    casper.test.done();

More asynchronously:

::

    casper.start('http://mydomain.tld/', function() {
        this.test.assertTitle('myTitle');
    });

    casper.thenClick('#logo', function() {
        this.test.assertUrlMatches(/mydomain/);
    });

    casper.run(function() {
        this.test.done();
    });

Added in 1.0 The ``expected`` parameter checks for an expected number of
performed assertions:

::

    casper.start('http://mydomain.tld/', function() {
        this.test.assertTitle('myTitle');
    });

    casper.thenClick('#logo', function() {
        this.test.assertUrlMatches(/mydomain/);
    });

    casper.run(function() {
        this.test.done(2);
    });

That's especially useful in case a given test script is abruptly
interrupted leaving you with no obvious way to know it and an
erroneously successful status.

.. raw:: html

   <h3 id="tester.error">

Tester#error(String message)

.. raw:: html

   </h3>

Writes an error-style formatted message to stdout.

::

    casper.test.error("Hi, I'm an error");

.. raw:: html

   <h3 id="tester.fail">

Tester#fail(String message)

.. raw:: html

   </h3>

Adds a failed test entry to the stack.

::

    casper.test.fail("Georges W. Bush");

.. raw:: html

   <h3 id="tester.formatMessage">

Tester#formatMessage(String message, String style)

.. raw:: html

   </h3>

Formats a message to highlight some parts of it. Only used internally by
the tester.

.. raw:: html

   <h3 id="tester.getFailures">

Tester#getFailures()

.. raw:: html

   </h3>

Added in 1.0 Retrieves failures for current test suite.

::

    casper.test.assertEquals(true, false);
    require('utils').dump(casper.test.getFailures());
    casper.test.done();

That will give something like this:

::

    $ casperjs test test-getFailures.js
    Test file: test-getFailures.js
    FAIL Subject equals the expected value
    #    type: assertEquals
    #    subject: true
    #    expected: false
    {
        "length": 1,
        "cases": [
            {
                "success": false,
                "type": "assertEquals",
                "standard": "Subject equals the expected value",
                "file": "test-getFailures.js",
                "values": {
                    "subject": true,
                    "expected": false
                }
            }
        ]
    }
    FAIL 1 tests executed, 0 passed, 1 failed.

    Details for the 1 failed test:

    In c.js:0
       assertEquals: Subject equals the expected value

.. raw:: html

   <h3 id="tester.getPasses">

Tester#getPasses()

.. raw:: html

   </h3>

Added in 1.0 Retrieves a report for successful test cases in the current
test suite.

::

    casper.test.assertEquals(true, true);
    require('utils').dump(casper.test.getPasses());
    casper.test.done();

That will give something like this:

::

    $ casperjs test test-getPasses.js
    Test file: test-getPasses.js
    PASS Subject equals the expected value
    {
        "length": 1,
        "cases": [
            {
                "success": true,
                "type": "assertEquals",
                "standard": "Subject equals the expected value",
                "file": "test-getPasses.js",
                "values": {
                    "subject": true,
                    "expected": true
                }
            }
        ]
    }
    PASS 1 tests executed, 1 passed, 0 failed.

.. raw:: html

   <h3 id="tester.info">

Tester#info(String message)

.. raw:: html

   </h3>

Writes an info-style formatted message to stdout.

::

    casper.test.info("Hi, I'm an informative message.");

.. raw:: html

   <h3 id="tester.pass">

Tester#pass(String message)

.. raw:: html

   </h3>

Adds a successful test entry to the stack.

::

    casper.test.pass("Barrack Obama");

.. raw:: html

   <h3 id="tester.renderResults">

Tester#renderResults(Boolean exit, Number status, String save)

.. raw:: html

   </h3>

Render tests results, save results in an XUnit formatted file, and
optionally exit phantomjs.

::

    var casper = require('casper').create();
    // ...
    casper.run(function() {
        // exists with status code 0 and saves XUnit formatted results
        // in test-results.xml
        this.test.renderResults(true, 0, 'test-results.xml');
    });

Note This method is not to be called when using the ```casperjs test``
command <testing.html#casper-test-command>`_, where it's done
automatically for you.
