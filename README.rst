==========
PyScaffold
==========

.. image:: https://travis-ci.org/blue-yonder/pyscaffold.svg?branch=master
    :target: https://travis-ci.org/blue-yonder/pyscaffold
.. image:: https://coveralls.io/repos/blue-yonder/pyscaffold/badge.png
    :target: https://coveralls.io/r/blue-yonder/pyscaffold
.. image:: https://requires.io/github/blue-yonder/pyscaffold/requirements.png?branch=master
     :target: https://requires.io/github/blue-yonder/pyscaffold/requirements/?branch=master
     :alt: Requirements Status
.. image:: https://badges.gitter.im/Join%20Chat.svg
   :alt: Join the chat at https://gitter.im/blue-yonder/pyscaffold
   :target: https://gitter.im/blue-yonder/pyscaffold?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

PyScaffold helps you to easily setup a new Python project, it is as easy as::

    putup my_project
    
This will create a new subdirectory ``my_project`` and serve you a project
setup with git repository, setup.py, document and test folder ready for some
serious coding.

Type ``putup -h`` to learn about more configuration options. PyScaffold assumes 
that you have `Git  <http://git-scm.com/>`_ installed and set up on your PC, 
meaning at least your name and email configured.
The scaffold of ``my_project`` provides you with following features:


Configuration & Packaging
=========================

All configuration can be done in ``setup.cfg`` like changing the description,
url, classifiers and even console scripts of your project. That means in most
cases it is not necessary to tamper with ``setup.py``.

In order to build a source, binary or wheel distribution, just run
``python setup.py sdist``, ``python setup.py bdist`` or
``python setup.py bdist_wheel``.

.. rubric:: Namespace Packages

Optionally, `namespace packages <http://pythonhosted.org/setuptools/setuptools.html#namespace-packages>`_
can be used, if you are planning to distribute a larger package as a collection
of smaller ones. For example, use::

    putup my_project --package my_package --with-namespace com.my_domain

to define ``my_package`` inside the namespace ``com.my_domain`` in java-style.

.. rubric:: Package and Files Data

Additional data inside your package (``package_data``) or in the root
directory of your project (``data_files``) can be configured in ``setup.cfg``.
To read this data in your code, use::

    from pkgutil import get_data
    data = get_data('my_package', 'path/to/my/data.txt')


Complete Git Integration
========================

Your project is already an initialised Git repository and ``setup.py`` uses
the information of tags to infer the version of your project.
To use this feature you need to tag with the format ``vMAJOR.MINOR[.REVISION]``
, e.g. ``v0.0.1`` or ``v0.1``. The prefix ``v`` is needed!
Run ``python setup.py version`` to retrieve the current `PEP440
<http://www.python.org/dev/peps/pep-0440/>`_-compliant version. This version
will be used when building a package and is also accessible through
``my_project.__version__``.

Unleash the power of Git by using its `pre-commit hooks
<http://pre-commit.com/>`_. This feature is available through the
``--with-pre-commit`` flag. After your project's scaffold was generated, make
sure pre-commit is installed, e.g. ``pip install pre-commit``, then just run
``pre-commit install``.

It goes unsaid that also a default ``.gitignore`` file is provided that is well
adjusted for Python projects and the most common tools.


Sphinx Documentation
====================

Build the documentation with ``python setup.py docs`` and run doctests with
``python setup.py doctest``. Start editing the file ``docs/index.rst`` to
extend the documentation. The documentation also works with `Read the Docs
<https://readthedocs.org/>`_.

In order to use the `numpydoc
<https://github.com/numpy/numpy/blob/master/doc/HOWTO_DOCUMENT.rst.txt>`_
documentation style, the flag ``--with-numpydoc`` can be specified.


Unittest & Coverage
===================

Run ``python setup.py test`` to run all unittests defined in the subfolder
``tests`` with the help of `py.test <http://pytest.org/>`_ and
`pytest-runner <https://pypi.python.org/pypi/pytest-runner>`_. Some sane
default flags for py.test are already defined in the ``[pytest]`` section of
``setup.cfg``. The py.test plugin
`pytest-cov <https://github.com/schlamar/pytest-cov>`_ is used to automatically
generate a coverage report. It is also possible to provide additional
parameters and flags on the commandline, e.g., type::

    python setup.py test --addopts -h

to show the help of py.test.

.. rubric:: JUnit and Coverage HTML/XML

For usage with a continuous integration software JUnit and Coverage XML output
can be activated in ``setup.cfg``. Use the flag ``--with-travis`` to generate
templates of the `Travis <https://travis-ci.org/>`_ configuration files
``.travis.yml`` and ``tests/travis_install.sh`` which even features the
coverage and stats system `Coveralls <https://coveralls.io/>`_.
In order to use the virtualenv management and test tool `Tox
<https://tox.readthedocs.org/>`_ the flag ``--with-tox`` can be specified.


Requirements Management
=======================

Add the requirements of your project to the ``requirements.txt`` file which
will be automatically used by ``setup.py``.
This also allows you to easily customize a plain virtual environment with::

    pip install -r requirements.txt


Licenses
========

All licenses from `choosealicense.com <http://choosealicense.com/>`_ can be
easily selected with the help of the ``--license`` flag.


Django
======

Create a `Django project <https://www.djangoproject.com/>`_ with the flag
``--with-django`` which is equivalent to
``django-admin.py startproject my_project`` enhanced by PyScaffold's features.


Cookiecutter
============

With the help of `Cookiecutter <https://cookiecutter.readthedocs.org/>`_ it
is possible to customize your project setup. Just use the flag
``--with-cookiecutter TEMPLATE`` to use a cookiecutter template which will be
refined by PyScaffold afterwards.


Easy Updating
=============

Keep your project's scaffold up-to-date by applying
``putput --update my_project`` when a new version of PyScaffold was released.
An update will only overwrite files that are not often altered by users like
setup.py. To update all files use ``--update --force``.
An existing project that was not setup with PyScaffold can be converted with
``putup --force existing_project``. The force option is completely safe to use
since the git repository of the existing project is not touched!

.. note::

    If you are updating from a PyScaffold version before 2.0, you must
    manually remove the files ``versioneer.py`` and ``MANIFEST.in``.
