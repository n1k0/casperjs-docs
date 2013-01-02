.. _tester_module:

.. index:: Testing

=====================
The ``tester`` module
=====================

Casper ships with a ``tester`` module and a ``Tester`` class providing an API for unit & functional testing purpose. By default you can access an instance of this class through the ``test`` property of any ``Casper`` class instance.

.. note::

   The best way to learn how to use the Tester API and see it in action is probably to have a look at `CasperJS' own test suites <https://github.com/n1k0/casperjs/blob/master/tests/suites/>`_.


The ``Tester`` prototype
++++++++++++++++++++++++

``assert()``
-------------------------------------------------------------------------------

**Signature:** ``assert(Boolean condition[, String message])``

Asserts that the provided condition strictly resolves to a boolean ``true``::

    casper.test.assert(true, "true's true");
    casper.test.assert(!false, "truth is out");

.. index:: DOM

``assertDoesntExist()``
-------------------------------------------------------------------------------

**Signature:** ``assertDoesntExist(String selector[, String message])``

Asserts that an element matching the provided :ref:`selector expression <selectors>` doesn't exists within the remote DOM environment::

    casper.start('http://www.google.fr/', function() {
        test.assertDoesntExist('form[name="gs"]', 'google.fr has a form with name "gs"');
    });

``assertEquals()``
-------------------------------------------------------------------------------

**Signature:** ``assertEquals(mixed testValue, mixed expected[, String message])``

Asserts that two values are strictly equals::

    var url = 'http://www.google.fr/';
    casper.start(url, function() {
        this.test.assertEquals(this.getCurrentUrl(), url, 'url is the one expected');
    });

.. index:: evaluate

``assertEval()``
-------------------------------------------------------------------------------

**Signature:** ``assertEval(Function fn[, String message, Mixed arguments])``

Asserts that a :ref:`code evaluation in remote DOM <casper_evaluate>` strictly resolves to a boolean ``true``::

    casper.start('http://www.google.fr/', function() {
        this.test.assertEval(function() {
            return __utils__.findAll('form').length > 0;
        }, 'google.fr has at least one form');
        this.test.assertEval(function(title) {
            return document.title === title;
        }, 'google.fr title is "Google"', 'Google');
    });

``assertEvalEquals()``
-------------------------------------------------------------------------------

**Signature:** ``assertEvalEquals(Function fn, mixed expected[, String message, Mixed arguments])``

Asserts that the result of a :ref:`code evaluation in remote DOM <casper_evaluate>` strictly equals to the expected value::

    casper.start('http://www.google.fr/', function() {
        this.test.assertEvalEquals(function() {
            return __utils__.findAll('form').length;
        }, 1, 'google.fr provides a single form tag');
        this.test.assertEval(function(title) {
            return document.title;
        }, 'Google', 'google.fr title is "Google"');
    });

.. _tester_assertelementcount:

``assertElementCount()``
-------------------------------------------------------------------------------

**Signature:** ``assertElementCount(String selector, Number count[, String message])``

Asserts that a :ref:`selector expression <selectors>` matches a given number of elements::

    casper.test.begin('assertElementCount() tests', 3, function(test) {
        casper.start().then(function() {
            this.page.content = '<ul><li>1</li><li>2</li><li>3</li></ul>';
            test.assertElementCount('ul', 1);
            test.assertElementCount('li', 3);
            test.assertElementCount('address', 0);
        }).run(function() {
            test.done();
        });
    });

.. index:: DOM

``assertExists()``
-------------------------------------------------------------------------------

**Signature:** ``assertExists(String selector[, String message])``

Asserts that an element matching the provided :ref:`selector expression <selectors>` exists in remote DOM environment::

    casper.start('http://www.google.fr/', function() {
        this.test.assertExists('form[name="gs"]', 'google.fr has a form with name "gs"');
    });

.. index:: falsiness

``assertFalsy()``
-------------------------------------------------------------------------------

**Signature:** ``assertFalsy(Mixed subject[, String message])``

.. versionadded:: 1.0

Asserts that a given subject is `falsy <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. index:: Form

``assertField()``
-------------------------------------------------------------------------------

**Signature:** ``assertField(String inputName, String expected[, String message])``

Asserts that a given form field has the provided value::

    casper.start('http://www.google.fr/', function() {
        this.fill('form[name="gs"]', { q: 'plop' }, false);
        this.test.assertField('q', 'plop');
    });

.. versionadded:: 1.0

This also works with any input type: ``select``, ``textarea``, etc.

.. index:: HTTP, HTTP Status Code

``assertHttpStatus()``
-------------------------------------------------------------------------------

**Signature:** ``assertHttpStatus(Number status[, String message])``

Asserts that current `HTTP status code <http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html>`_ is the same as the one passed as argument::

    casper.start('http://www.google.fr/', function() {
        this.test.assertHttpStatus(200, 'google.fr is up');
    });

``assertMatch()``
-------------------------------------------------------------------------------

**Signature:** ``assertMatch(mixed subject, RegExp pattern[, String message])``

Asserts that a provided string matches a provided javascript ``RegExp`` pattern::

    casper.test.assertMatch('Chuck Norris', /^chuck/i, 'Chuck Norris' first name is Chuck');

``assertNot()``
-------------------------------------------------------------------------------

**Signature:** ``assertNot(mixed subject[, String message])``

Asserts that the passed subject resolves to some `falsy value <http://11heavens.com/falsy-and-truthy-in-javascript>`_::

    casper.test.assertNot(false, "Universe is still operational");

``assertNotEquals()``
-------------------------------------------------------------------------------

**Signature:** ``assertNotEquals(mixed testValue, mixed expected[, String message])``

.. versionadded:: 0.6.7

Asserts that two values are **not** strictly equals::

    casper.test.assertNotEquals(true, "Truth is out");

``assertNotVisible()``
-------------------------------------------------------------------------------

**Signature:** ``assertNotVisible(String selector[, String message])``

Asserts that the element matching the provided :ref:`selector expression <selectors>` is not visible::

    casper.start('http://www.google.fr/', function() {
        this.test.assertNotVisible('h6');
    });

.. index:: error

``assertRaises()``
-------------------------------------------------------------------------------

**Signature:** ``assertRaises(Function fn, Array args[, String message])``

Asserts that the provided function called with the given parameters raises a javascript ``Error``::

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

``assertSelectorDoesntHaveText()``
-------------------------------------------------------------------------------

**Signature:** ``assertSelectorDoesntHaveText(String selector, String text[, String message])``

Asserts that given text does not exist in all the elements matching the provided :ref:`selector expression <selectors>`::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorDoesntHaveText('title', 'Yahoo!');
    });

.. index:: selector, DOM

``assertSelectorExists()``
-------------------------------------------------------------------------------

**Signature:** ``assertSelectorExists(String selector[, String message])``

Asserts that at least an element matching the provided :ref:`selector expression <selectors>` exists in remote DOM::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorExists('form[name="gs"]', 'google.fr provides a form');
    });

``assertSelectorHasText()``
-------------------------------------------------------------------------------

**Signature:** ``assertSelectorHasText(String selector, String text[, String message])``

Asserts that given text exists in elements matching the provided :ref:`selector expression <selectors>`::

    casper.start('http://www.google.fr/', function() {
        this.test.assertSelectorHasText('title', 'Google');
    });

.. index:: HTTP

``assertResourceExists()``
-------------------------------------------------------------------------------

**Signature:** ``assertResourceExists(Function testFx[, String message])``

The ``testFx`` function is executed against all loaded assets and the test passes when at least one resource matches::

    casper.start('http://www.google.fr/', function() {
        this.test.assertResourceExists(function (resource) {
          return resource.url.match('logo3w.png');
        }, 'google.fr logo was loaded');
        // or shorter
        this.test.assertResourceExists('logo3w.png', 'google.fr logo was loaded');
    });

.. hint::

   Check the documentation for :ref:`Casper.resourceExists() <casper_resourceexists>`.

``assertTextExists()``
-------------------------------------------------------------------------------

**Signature:** ``assertTextExists(String expected[, String message])``

Asserts that body **plain text content** contains the given string::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTextExists('google', 'page body contains "google"');
    });

``assertTextDoesntExist()``
-------------------------------------------------------------------------------

**Signature:** ``assertTextDoesntExist(String unexpected[, String message])``

.. versionadded:: 1.0

Asserts that body **plain text content** doesn't contain the given string::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTextDoesntExist('bing', 'page body does not contain "bing"');
    });

``assertTitle()``
-------------------------------------------------------------------------------

**Signature:** ``assertTitle(String expected[, String message])``

Asserts that title of the remote page equals to the expected one::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTitle('Google', 'google.fr has the correct title');
    });

``assertTitleMatch()``
-------------------------------------------------------------------------------

**Signature:** ``assertTitleMatch(RegExp pattern[, String message])``

Asserts that title of the remote page matches the provided RegExp pattern::

    casper.start('http://www.google.fr/', function() {
        this.test.assertTitleMatch(/Google/, 'google.fr has a quite predictable title');
    });

.. index:: truthiness

``assertTruthy()``
-------------------------------------------------------------------------------

**Signature:** ``assertTruthy(Mixed subject[, String message])``

.. versionadded:: 1.0

Asserts that a given subject is `truthy <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. index:: Type

``assertType()``
-------------------------------------------------------------------------------

**Signature:** ``assertType(mixed input, String type[, String message])``

Asserts that the provided input is of the given type::

    casper.test.assertType(42, "number", "Okay, 42 is a number");
    casper.test.assertType([1, 2, 3], "array", "Yeah, we can test for arrays too =)");

.. index:: URL

``assertUrlMatch()``
-------------------------------------------------------------------------------

**Signature:** ``assertUrlMatch(Regexp pattern[, String message])``

Asserts that a the current page url matches the provided RegExp pattern::

    casper.start('http://www.google.fr/', function() {
        this.test.assertUrlMatch(/^http:\/\//', 'google.fr is served in http://');
    });

.. index:: DOM

``assertVisible()``
-------------------------------------------------------------------------------

**Signature:** ``assertVisible(String selector[, String message])``

Asserts that the element matching the provided :ref:`selector expression <selectors>` is visible::

    casper.start('http://www.google.fr/', function() {
        this.test.assertVisible('h1');
    });

.. _tester_begin:

.. index:: Test suite, planned tests, Asynchronicity, Termination

``begin()``
-------------------------------------------------------------------------------

**Signature:** ``begin(String description, Number planned, Function suite)``

.. versionadded:: 1.1

Starts a suite of ``<planned>`` tests. The ``suite`` callback will get the current ``Tester`` instance as its first argument::

    function Cow() {
        this.mowed = false;
        this.moo = function moo() {
            this.mowed = true; // mootable state: don't do that
            return 'moo!';
        };
    }

    // unit style synchronous test case
    casper.test.begin('Cow can moo', 2, function suite(test) {
        var cow = new Cow();
        test.assertEquals(cow.moo(), 'moo!');
        test.assert(cow.mowed);
        test.done();
    });

.. note::

   The ``planned`` argument is especially useful in case a given test script is abruptly interrupted leaving you with no obvious way to know it and an erroneously successful status.

A more asynchronous example::

    casper.test.begin('Casperjs.org is navigable', 2, function suite(test) {
        casper.start('http://casperjs.org/', function() {
            test.assertTitleMatches(/casperjs/i);
            this.clickLabel('Testing');
        });

        casper.then(function() {
            test.assertUrlMatches(/testing\.html$/);
        });

        casper.run(function() {
            test.done();
        });
    });

.. important::

   `done()`_ **must** be called in order to terminate the suite. This is specially important when doing asynchronous tests so ensure it's called when everything has actually been performed.

.. index:: Colors

``colorize()``
-------------------------------------------------------------------------------

**Signature:** ``colorize(String message, String style)``

Render a colorized output. Basically a proxy method for ``Casper.Colorizer#colorize()``.

``comment()``
-------------------------------------------------------------------------------

**Signature:** ``comment(String message)``

Writes a comment-style formatted message to stdout::

    casper.test.comment("Hi, I'm a comment");

.. _tester_done:

.. index:: Test suite, Asynchronicity, Termination, done()

``done()``
-------------------------------------------------------------------------------

**Signature:** ``done()``

.. versionchanged:: 1.1 ``planned`` parameter is deprecated

Flag a test suite started with `begin()`_ as processed::

    casper.test.begin('my test suite', 2, function(test) {
        test.assert(true);
        test.assertNot(false);
        test.done();
    });

More asynchronously::

    casper.test.begin('Casperjs.org is navigable', 2, function suite(test) {
        casper.start('http://casperjs.org/', function() {
            test.assertTitleMatches(/casperjs/i);
            this.clickLabel('Testing');
        });

        casper.then(function() {
            test.assertUrlMatches(/testing\.html$/);
        });

        casper.run(function() {
            test.done();
        });
    });

``error()``
-------------------------------------------------------------------------------

**Signature:** ``error(String message)``

Writes an error-style formatted message to stdout::

    casper.test.error("Hi, I'm an error");

.. index:: Test failure

``fail()``
-------------------------------------------------------------------------------

**Signature:** ``fail(String message)``

Adds a failed test entry to the stack::

    casper.test.fail("Georges W. Bush");

``formatMessage()``
-------------------------------------------------------------------------------

**Signature:** ``formatMessage(String message, String style)``

Formats a message to highlight some parts of it. Only used internally by the tester.

``getFailures()``
-------------------------------------------------------------------------------

**Signature:** ``getFailures()``

.. versionadded:: 1.0

Retrieves failures for current test suite::

    casper.test.assertEquals(true, false);
    require('utils').dump(casper.test.getFailures());
    casper.test.done();

That will give something like this:

.. code-block:: text

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

``getPasses()``
-------------------------------------------------------------------------------

**Signature:** ``getPasses()``

.. versionadded:: 1.0

Retrieves a report for successful test cases in the current test suite::

    casper.test.assertEquals(true, true);
    require('utils').dump(casper.test.getPasses());
    casper.test.done();

That will give something like this::

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

``info()``
-------------------------------------------------------------------------------

**Signature:** ``info(String message)``

Writes an info-style formatted message to stdout::

    casper.test.info("Hi, I'm an informative message.");

.. index:: Test success

``pass()``
-------------------------------------------------------------------------------

**Signature:** ``pass(String message)``

Adds a successful test entry to the stack::

    casper.test.pass("Barrack Obama");

``renderResults()``
-------------------------------------------------------------------------------

**Signature:** ``renderResults(Boolean exit, Number status, String save)``

Render tests results, save results in an XUnit formatted file, and optionally exits phantomjs::

    casper.test.renderResults(true, 0, 'test-results.xml');

.. note::

   This method is not to be called when using the ``casperjs test`` command (see documentation for :doc:`testing <../testing>`), where it's done automatically for you.
