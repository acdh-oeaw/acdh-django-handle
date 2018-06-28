=============================
acdh-django-handle
=============================

.. image:: https://badge.fury.io/py/acdh-django-handle.svg
    :target: https://badge.fury.io/py/acdh-django-handle

.. image:: https://travis-ci.org/acdh-oeaw/acdh-django-handle.svg?branch=master
    :target: https://travis-ci.org/acdh-oeaw/acdh-django-handle

.. image:: https://codecov.io/gh/acdh-oeaw/acdh-django-handle/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/acdh-oeaw/acdh-django-handle

A django app to create and manage handle-pids

Documentation
-------------

The full documentation is at https://acdh-django-handle.readthedocs.io.

Quickstart
----------

Install acdh-django-handle::

    pip install acdh-django-handle

Add it to your `INSTALLED_APPS`:

.. code-block:: python

    INSTALLED_APPS = (
        ...
        'handle',
        ...
    )


Features
--------

* TODO

Running Tests
-------------

Does the code actually work?

::

    source <YOURVIRTUALENV>/bin/activate
    (myenv) $ pip install tox
    (myenv) $ tox

Credits
-------

Tools used in rendering this package:

*  Cookiecutter_
*  `cookiecutter-djangopackage`_

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`cookiecutter-djangopackage`: https://github.com/pydanny/cookiecutter-djangopackage
