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
