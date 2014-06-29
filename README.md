django-admin-resumable-js
=========================

django-admin-resumable-js is a django app to allow you to upload large files from within the django admin site.

Screenshot
----------
![Image](screenshot.png?raw=true)


Installation
------------

* Add ```admin_resumable``` to your ```INSTALLED_APPS```
* Add ```url(r'^admin_resumable/', include('admin_resumable.urls')),``` to your urls.py
* Add a model field eg:
```from admin_resumable.fields import ModelAdminResumableFileField```

```python
class Foo(models.Model):
  bar = models.CharField(max_length=200)
  foo = ModelAdminResumableFileField()
```

Optionally:

* Set ``ADMIN_RESUMABLE_SUBDIR``, default is ``'admin_uploaded'``
* Set ``ADMIN_RESUMABLE_CHUNKSIZE``, default is ``"1*1024*1024"``
* Set ``ADMIN_RESUMABLE_FILESYSTEM_STORAGE``, default is ``'django.core.files.storage.FileSystemStorage'`` (must be a subclass of ``django.core.files.storage.FileSystemStorage``, or accept the ``location`` init parameter).  If you don't want the default FileSystemStorage behaviour of creating new files on the server with filenames appended with _1, _2, etc for consecutive uploads of the same file, then you could use this to set your storage class to something like https://djangosnippets.org/snippets/976/


South
-----

If you use South for migration, then put this at the top of your models.py file to help South introspect your ``ModelAdminResumableFileField``:

```python
from south.modelsinspector import add_introspection_rules

add_introspection_rules([], [
    r'^admin_resumable\.fields\.ModelAdminResumableFileField'])


Todo
----

* Testing

Thanks to
---------

Resumable.js https://github.com/23/resumable.js

django-resumable https://github.com/jeanphix/django-resumable
