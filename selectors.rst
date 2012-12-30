.. _selectors:

=========
Selectors
=========

CasperJS makes an heavy use of selectors in order to work with the
`DOM <http://www.w3.org/TR/dom/>`_, and can transparently use either
`CSS3 <http://www.w3.org/TR/selectors/>`_ or
`XPath <http://www.w3.org/TR/xpath/>`_ expressions.

CSS3
----

By default, Casper will accept `CSS3 selector
strings <http://www.w3.org/TR/selectors/#selectors>`_ to check for
elements within the DOM. For example, to check if a ``<div id="plop">``
element exists in a page, you can use:

::

    casper.start('http://domain.tld/page.html', function() {
        this.test.assertExists('#plop', 'the element exists');
    });

XPath
-----

Added in 0.6.8 You can alternatively use `XPath expression strings <>`_
instead:

::

    casper.thenOpen('http://domain.tld/page.html', function() {
        this.test.assertExists({
            type: 'xpath',
            path: '//*[@id="plop"]'
        }, 'the element exists');
    });

To ease the use and reading of XPath expressions, a ``selectXPath``
helper is available from the ``casper`` module:

::

    var x = require('casper').selectXPath;

    casper.thenOpen('http://domain.tld/page.html', function() {
        this.test.assertExists(x('//*[@id="plop"]'), 'the element exists');
    });

Warning The only limitation of XPath use in CasperJS is in the
```fill()`` <api.html#casper.fill>`_ method when you want to fill **file
fields**; PhantomJS natively only allows the use of CSS3 selectors in
its uploadFile method, hence this limitation.
