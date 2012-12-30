.. _colorizer_module:

========================
The ``colorizer`` module
========================

Casper ships with a ``colorizer`` module which contains a ``Colorizer``
class which can print stuff to the console output in color:

::

    var colorizer = require('colorizer').create('Colorizer');
    console.log(colorizer.colorize("Hello World", "INFO"));

Though most of the times you will use it transparently using the
```Casper.echo()`` <api.html#echo>`_ method:

::

    casper.echo('an informative message', 'INFO'); // printed in green
    casper.echo('an error message', 'ERROR');      // printed in red

.. raw:: html

   <h3 id="colorizer.Dummy">

Skipping CasperJS styling operations

.. raw:: html

   </h3>

If you wish to skip the whole coloration operation and get uncolored
plain text, just set the ``colorizerType`` casper option to ``Dummy``:

::

    var casper = require('casper').create({
        colorizerType: 'Dummy'
    });

    casper.echo("Hello", "INFO");

Note That's especially useful if you're using CasperJS on the Windows
platform, as there's no support for colored output on this platform.

.. raw:: html

   <h3 id="colorizer.styles">

Available predefined styles

.. raw:: html

   </h3>

Available predefined styles are:

-  ``ERROR``: white text on red background
-  ``INFO``: green text
-  ``TRACE``: green text
-  ``PARAMETER``: cyan text
-  ``COMMENT``: yellow text
-  ``WARNING``: red text
-  ``GREEN_BAR``: white text on green background
-  ``RED_BAR``: white text on red background
-  ``INFO_BAR``: cyan text

Here's a sample output of what it can look like:

.. figure:: images/colorizer.png
   :align: center
   :alt: capture

   capture

.. raw:: html

   <h3 id="colorizer.colorize">

Colorizer#colorize(String text, String styleName)

.. raw:: html

   </h3>

Computes a colored version of the provided text string using a given
predefined style.

::

    var colorizer = require('colorizer').create();
    console.log(colorizer.colorize("I'm a red error", "ERROR"));

Note Most of the time you won't have to use a ``Colorizer`` instance
directly as CasperJS provides all the necessary methods.

See the list of the `predefined styles available <#colorizer.styles>`_.

.. raw:: html

   <h3 id="colorizer.format">

Colorizer#format(String text, Object style)

.. raw:: html

   </h3>

Formats a text string using the provided style definition. A style
definition is a standard javascript ``Object`` instance which can define
the following properties:

-  String ``bg``: background color name
-  String ``fg``: foreground color name
-  Boolean ``bold``: apply bold formatting
-  Boolean ``underscore``: apply underline formatting
-  Boolean ``blink``: apply blink formatting
-  Boolean ``reverse``: apply reverse formatting
-  Boolean ``conceal``: apply conceal formatting

Note Available color names are ``black``, ``red``, ``green``,
``yellow``, ``blue``, ``magenta``, ``cyan`` and ``white``.

::

    var colorizer = require('colorizer').create();
    colorizer.format("We all live in a yellow submarine", {
        bg:   'yellow',
        fg:   'blue',
        bold: true
    });

