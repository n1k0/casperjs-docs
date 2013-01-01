.. _utils_module:

====================
The ``utils`` module
====================

This module provide simple helper functions, some of them being very specific to CasperJS though.

Functions reference
+++++++++++++++++++

The ``utils`` module contains simple functions which circumvent some lacks in the standard Javascript API.

Usage is pretty much straightforward::

    var utils = require('utils');

    utils.dump({plop: 42});

``betterTypeOf()``
--------------------------------------------------------------------------------

**Signature:** ``betterTypeOf(input)``

Provides a better ``typeof`` operator equivalent, eg. able to retrieve the ``Array`` type.

``dump()``
--------------------------------------------------------------------------------

**Signature:** ``dump(value)``

Dumps a JSON representation od passed argument onto the standard output. Useful for :doc:`debugging <../debugging>`.

``fileExt()``
--------------------------------------------------------------------------------

**Signature:** ``fileExt(file)``

Retrieves the extension of passed filename.

``fillBlanks()``
--------------------------------------------------------------------------------

**Signature:** ``fillBlanks(text, pad)``

Fills a string with trailing spaces to match ``pad`` length.

``format()``
--------------------------------------------------------------------------------

**Signature:** ``format(f)``

Formats a string against passed args. ``sprintf`` equivalent.

Note This is a port of nodejs ``util.format()``.

``getPropertyPath()``
--------------------------------------------------------------------------------

**Signature:** ``getPropertyPath(Object obj, String path)``

Added in 1.0 Retrieves the value of an Object foreign property using a dot-separated path string::

    var account = {
        username: 'chuck',
        skills: {
            kick: {
                roundhouse: true
            }
        }
    }
    utils.getPropertyPath(account, 'skills.kick.roundhouse'); // true

**Beware, this function doesn't handle object key names containing a dot.**

``inherits()``
--------------------------------------------------------------------------------

**Signature:** ``inherits(ctor, superCtor)``

Makes a constructor inheriting from another. Useful for subclassing and :doc:`extending <../extending>`.

.. note::

   This is a port of nodejs ``util.inherits()``.

``isArray()``
--------------------------------------------------------------------------------

**Signature:** ``isArray(value)``

Checks if passed argument is an instance of ``Array``.

``isCasperObject()``
--------------------------------------------------------------------------------

**Signature:** ``isCasperObject(value)``

Checks if passed argument is an instance of ``Casper``.

``isClipRect()``
--------------------------------------------------------------------------------

**Signature:** ``isClipRect(value)``

Checks if passed argument is a ``cliprect`` object.

``isFalsy()``
--------------------------------------------------------------------------------

**Signature:** ``isFalsy(subject)``

Added in 1.0 Returns subject `falsiness <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

``isFunction()``
--------------------------------------------------------------------------------

**Signature:** ``isFunction(value)``

Checks if passed argument is a function.

``isJsFile()``
--------------------------------------------------------------------------------

**Signature:** ``isJsFile(file)``

Checks if passed filename is a Javascript one (by checking if it has a ``.js`` or ``.coffee`` file extension).

``isNull()``
--------------------------------------------------------------------------------

**Signature:** ``isNull(value)``

Checks if passed argument is a ``null``.

``isNumber()``
--------------------------------------------------------------------------------

**Signature:** ``isNumber(value)``

Checks if passed argument is an instance of ``Number``.

``isObject()``
--------------------------------------------------------------------------------

**Signature:** ``isObject(value)``

Checks if passed argument is an object.

``isString()``
--------------------------------------------------------------------------------

**Signature:** ``isString(value)``

Checks if passed argument is an instance of ``String``.

``isTruthy()``
--------------------------------------------------------------------------------

**Signature:** ``isTruthy(subject)``

Added in 1.0 Returns subject `truthiness <http://11heavens.com/falsy-and-truthy-in-javascript>`_.

``isType()``
--------------------------------------------------------------------------------

**Signature:** ``isType(what, type)``

Checks if passed argument has its type matching the ``type`` argument.

``isUndefined()``
--------------------------------------------------------------------------------

**Signature:** ``isUndefined(value)``

Checks if passed argument is ``undefined``.

``isWebPage()``
--------------------------------------------------------------------------------

**Signature:** ``isWebPage(what)``

Checks if passed argument is an instance of native PhantomJS' ``WebPage`` object.

``mergeObjects()``
--------------------------------------------------------------------------------

**Signature:** ``mergeObjects(origin, add)``

Merges two objects recursively.

``node()``
--------------------------------------------------------------------------------

**Signature:** ``node(name, attributes)``

Creates an (HT\|X)ML element, having optional ``attributes`` added.

``serialize()``
--------------------------------------------------------------------------------

**Signature:** ``serialize(value)``

Serializes a value using JSON format. Will serialize functions as strings. Useful for :doc:`debugging <../debugging>` and comparing objects.

``unique()``
--------------------------------------------------------------------------------

**Signature:** ``unique(array)``

Retrieves unique values from within a given ``Array``.
