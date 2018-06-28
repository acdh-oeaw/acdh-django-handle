=============================
acdh-django-handle
=============================

.. image:: https://badge.fury.io/py/acdh-django-handle.svg
    :target: https://badge.fury.io/py/acdh-django-handle

.. image:: https://travis-ci.org/acdh-oeaw/acdh-django-handle.svg?branch=master
    :target: https://travis-ci.org/acdh-oeaw/acdh-django-handle

.. image:: https://codecov.io/gh/acdh-oeaw/acdh-django-handle/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/acdh-oeaw/acdh-django-handle

A django app to create and manage handle-pids.

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

Provide a handle-config dict:

.. code-block:: python

    HANDLE = {
        'resolver': "http://hdl.handle.net",
        'user': "your handle-provider user",
        'pw': "your handle-provider password",
        'url': "base url to your handle-provider api",
        'app_base_url': "the base url of your application"
    }

example:

.. code-block:: python

    HANDLE = {
        'resolver': "http://hdl.handle.net",
        'user': "user11.1234567-01",
        'pw': "password1234",
        'url': "http://pid.gwdg.de/handles/11.1234567-01/",
        'app_base_url': "https://myproject.com"
    }

The value of `app_base_url` will be concaneted with the value of the `get_absolute_url` method of the model instance you want to register a handle for.

And run

    python manage.py migrate handle


Create/register handle-pids
----

The package provides a management command to bulk create/register handle-pids. For this you'll have to
* add a `GenericRelation` property to the model class you would like register handles for
* and make sure you have a `get_absolute_url` method defined

.. code-block:: python

    from django.contrib.contenttypes.fields import GenericRelation

    ...

    class Example(models.Model):
        name = models.CharField(
            max_length=255, blank=True,
        )
        ...
        pid = GenericRelation(Pid, blank=True, null=True, related_query_name="get_pid")
        ...
        def get_absolute_url(self):
            return reverse('example_detail', kwargs={'pk': self.id})

To register/create handle-pids run:

    python manage.py crate_handles example

In case your GenericRelation property is named something else than `pid` you need to pass in the name as second argument, e.g:

    python manage.py crate_handles example --pid=<name>

Handle-Pids will only be crated for objects which do not have a handle-pid yet.


Features
--------

* Provides a `Pid` class which stores
  * a handle-pid
  * creation and modification date
  * a generic relation to any other class of your django project.
  * an overidden save-method which will register/create a handle-pid on save in case you didn't provide a handle-pid

* Provides a `handle.utils.create_handle` function to register/create a new handle-pid

* Register/Create handle-pid for any objects in your project via admin-interface.

* Provides a management command to bulk create/register handle-pids for all instances of a model-class in your project.


Credits
-------

Tools used in rendering this package:

*  Cookiecutter_
*  `cookiecutter-djangopackage`_

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`cookiecutter-djangopackage`: https://github.com/pydanny/cookiecutter-djangopackage
