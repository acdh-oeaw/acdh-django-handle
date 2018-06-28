=====
Usage
=====

To use acdh-django-handle in a project, add it to your `INSTALLED_APPS`:

.. code-block:: python

    INSTALLED_APPS = (
        ...
        'handle.apps.HandleConfig',
        ...
    )

Add acdh-django-handle's URL patterns:

.. code-block:: python

    from handle import urls as handle_urls


    urlpatterns = [
        ...
        url(r'^', include(handle_urls)),
        ...
    ]
