========
CasperJS
========

CasperJS is an open source navigation scripting & testing utility written in Javascript and based on PhantomJS_ — the scriptable headless WebKit_ engine.

.. figure:: _static/images/demo.png
   :align: center
   :alt:

It eases the process of **defining a full navigation scenario** and provides useful **high-level functions, methods & syntactic sugar** for doing common tasks such as:

- defining & ordering browsing `navigation steps <quickstart.html>`_
- filling & submitting `forms <api.html#casper.fill>`_
- `clicking <api.html#casper.click>`_ & following links
- capturing `screenshots <api.html#casper.captureSelector>`_ of a page (or part of it)
- `testing <api.html#tester>`_ remote DOM
- `logging <logging.html>`_ events
- `downloading <api.html#casper.download>`_ resources, including binary ones
- writing `functional test suites <testing.html>`_, saving results as JUnit XML
- `scraping <https://github.com/n1k0/casperjs/blob/master/samples/>`_ Web contents

Get started
===========

- `install CasperJS <installation.html>`_ and `get started <quickstart.html>`_
- browse the `samples repository <https://github.com/n1k0/casperjs/tree/master/samples>`_
- get the `code at Github <https://github.com/n1k0/casperjs>`_ and `contribute <https://github.com/n1k0/casperjs/blob/master/CONTRIBUTING.md#contribution-guide>`_
- read the `FAQ <faq.html>`_ and get `support <https://groups.google.com/forum/#!forum/casperjs>`_
- follow `@casperjs\_org <https://twitter.com/casperjs_org>`_ on Twitter

Index
=====

.. toctree::
    :maxdepth: 2

    overview
    installation
    quickstart
    license
    rst-syntax


API documentation
=================

These are guides and API documentation for the individual CasperJS core modules and extensions.

See the :ref:`genindex` if you are looking for the docs for a particular part of the API.

.. toctree::
    :maxdepth: 2

    modules/index

.. _PhantomJS: http://phantomjs.org/
.. _WebKit: http://www.webkit.org/
