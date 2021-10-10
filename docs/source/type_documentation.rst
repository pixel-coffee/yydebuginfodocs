Type Documentation
==================

This quick guide serves as a reference for how parameter/return types are documented in the API Reference.

Motivation
^^^^^^^^^^

GML is a dynamically-typed language. It does not support nominally-typed classes, often uses ID
numbers to represent objects and certain data structures, and has functions that can accept more than one
type of data. Because of this, it can be confusing knowing what type of data certain variables contain, or
what is accepted/returned by certain functions. This document attempts to alleviate that by enforcing
a particular standard when describing the data types of the functions detailed in the API Reference.

Generally speaking, the type terms have been chosen carefully such that it should be easy enough to
understand what is expected of the API without even needing this guide. However, in the event that the documented
type is unclear or creates confusion, this reference is here.

After reading this document, the goal is that you will be able to understand API type definitions like the following:

.. image:: images/api_types.png

Without any ambiguity.

Without further ado, the following is a list of the type terms that will be used throughout the API Reference:

Type Reference
^^^^^^^^^^^^^^

number
******

One of the simplest types to understand, the ``number`` type can be used to represent any real number, like ``1``, ``2``, ``-16.781``, or even ``infinity``.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "number"``.

string
******

The ``string`` type represents textual data, such as ``"John"``, ``"Player 2"``, or ``"The quick brown fox."``. The text in question can contain letters, digits, spaces, punctuation, or even unicode characters such as symbols from non-Latin-based languages.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "string"``.

bool
****

The ``bool`` type is a single bit of data that represents a ``true`` or a ``false``.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "bool"``.

int32
*****

The ``int32`` type represents an integer within the range `-2,147,483,648` to `2,147,483,647`.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "int32"``.

int64
*****

The ``int64`` type represents an integer within the range `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "int64"``.

ptr
***

The ``ptr`` type represents a reference to a location in physical memory, usually as a 32-bit or 64-bit integer.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "ptr"``.

undefined
*********

The ``undefined`` type is a `unit type <https://en.wikipedia.org/wiki/Unit_type>`_, whose value indicates that something is erroneous or invalid.
In the context of our API Reference, it refers specifically to the datatype of any variable where ``typeof(var_name) == "undefined"`` (and thus, ``var_name == undefined``).

