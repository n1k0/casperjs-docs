====================
The ``utils`` module
====================

The ``utils`` module contains simple functions which circumvent some
lacks in the standard Javascript API.

Usage is pretty much straightforward:

::

    var utils = require('utils');

    utils.dump({plop: 42});

.. raw:: html

   <h3 id="utils.betterTypeOf">

utils.betterTypeOf(input)

.. raw:: html

   </h3>

Provides a better ``typeof`` operator equivalent, able to retrieve the
``Array`` type.

.. raw:: html

   <h3 id="utils.dump">

utils.dump(value)

.. raw:: html

   </h3>

Dumps a JSON representation od passed argument onto the standard output.
Useful for `debugging <debugging.html>`_.

.. raw:: html

   <h3 id="utils.fileExt">

utils.fileExt(file)

.. raw:: html

   </h3>

Retrieves the extension of passed filename.

.. raw:: html

   <h3 id="utils.fillBlanks">

utils.fillBlanks(text, pad)

.. raw:: html

   </h3>

Fills a string with trailing spaces to match ``pad`` length.

.. raw:: html

   <h3 id="utils.format">

utils.format(f)

.. raw:: html

   </h3>

Formats a string against passed args. ``sprintf`` equivalent.

Note This is a port of nodejs ``util.format()``.

.. raw:: html

   <h3 id="utils.getPropertyPath">

utils.getPropertyPath(Object obj, String path)

.. raw:: html

   </h3>

Added in 1.0 Retrieves the value of an Object foreign property using a
dot-separated path string:

::

    var account = {
        username: 'chuck',
        skills: {
            kick: {
                roundhouse: true
            }
        }
    }
    utils.getPropertyPath(account, 'skills.kick.roundhouse'); // true

**Beware, this function doesn't handle object key names containing a
dot.**

.. raw:: html

   <h3 id="utils.inherits">

utils.inherits(ctor, superCtor)

.. raw:: html

   </h3>

Makes a constructor inheriting from another. Useful for subclassing and
`extending <extending.html>`_.

Note This is a port of nodejs ``util.inherits()``.

.. raw:: html

   <h3 id="utils.isArray">

utils.isArray(value)

.. raw:: html

   </h3>

Checks if passed argument is an instance of ``Array``.

.. raw:: html

   <h3 id="utils.isCasperObject">

utils.isCasperObject(value)

.. raw:: html

   </h3>

Checks if passed argument is an instance of ``Casper``.

.. raw:: html

   <h3 id="utils.isClipRect">

utils.isClipRect(value)

.. raw:: html

   </h3>

Checks if passed argument is a ``cliprect`` object.

.. raw:: html

   <h3 id="utils.isFalsy">

utils.isFalsy(subject)

.. raw:: html

   </h3>

Added in 1.0 Returns subject
`falsiness <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. raw:: html

   <h3 id="utils.isFunction">

utils.isFunction(value)

.. raw:: html

   </h3>

Checks if passed argument is a function.

.. raw:: html

   <h3 id="utils.isJsFile">

utils.isJsFile(file)

.. raw:: html

   </h3>

Checks if passed filename is a Javascript one (by checking if it has a
``.js`` or ``.coffee`` file extension).

.. raw:: html

   <h3 id="utils.isNull">

utils.isNull(value)

.. raw:: html

   </h3>

Checks if passed argument is a ``null``.

.. raw:: html

   <h3 id="utils.isNumber">

utils.isNumber(value)

.. raw:: html

   </h3>

Checks if passed argument is an instance of ``Number``.

.. raw:: html

   <h3 id="utils.isObject">

utils.isObject(value)

.. raw:: html

   </h3>

Checks if passed argument is an object.

.. raw:: html

   <h3 id="utils.isString">

utils.isString(value)

.. raw:: html

   </h3>

Checks if passed argument is an instance of ``String``.

.. raw:: html

   <h3 id="utils.isTruthy">

utils.isTruthy(subject)

.. raw:: html

   </h3>

Added in 1.0 Returns subject
`truthiness <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

.. raw:: html

   <h3 id="utils.isType">

utils.isType(what, type)

.. raw:: html

   </h3>

Checks if passed argument has its type matching the ``type`` argument.

.. raw:: html

   <h3 id="utils.isUndefined">

utils.isUndefined(value)

.. raw:: html

   </h3>

Checks if passed argument is ``undefined``.

.. raw:: html

   <h3 id="utils.isWebPage">

utils.isWebPage(what)

.. raw:: html

   </h3>

Checks if passed argument is an instance of native PhantomJS'
``WebPage`` object.

.. raw:: html

   <h3 id="utils.mergeObjects">

utils.mergeObjects(origin, add)

.. raw:: html

   </h3>

Merges two objects recursively.

.. raw:: html

   <h3 id="utils.node">

utils.node(name, attributes)

.. raw:: html

   </h3>

Creates an (HT\|X)ML element, having optional ``attributes`` added.

.. raw:: html

   <h3 id="utils.serialize">

utils.serialize(value)

.. raw:: html

   </h3>

Serializes a value using JSON format. Will serialize functions as
strings. Useful for `debugging <debugging.html>`_ and comparing objects.

.. raw:: html

   <h3 id="utils.unique">

utils.unique(array)

.. raw:: html

   </h3>

Retrieves unique values from within a given ``Array``.
