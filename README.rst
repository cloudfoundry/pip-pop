pip-pop
=======

.. image:: https://travis-ci.org/kennethreitz/pip-pop.svg?branch=master
    :target: https://travis-ci.org/kennethreitz/pip-pop

.. image:: https://raw.githubusercontent.com/cloudfoundry/pip-pop/master/docs/pop-pop.gif

Working with lots of ``requirements.txt`` files can be a bit annoying.
Have no fear, **pip-pop** is here!

(work in progress)

Planned Commands
----------------

``$ pip-diff [--fresh | --stale] <reqfile> <reqfile>``

Generates a diff between two given requirements files. Lists either stale or fresh packages.

``$ pip-grep <reqfile> <package>...``

Takes a requirements file, and searches for the specified package (or packages) within it.
Essential when working with included files.


Possible Future Commands
------------------------

- Install with blacklisting support (wsgiref, distribute, setuptools).

Development
-----------

To run the tests:

1. ``pip install -r requirements.txt``
2. ``tox``

Building artifact for buildpacks
--------------------------------

We need to create a tarball that contains a distribution of this repo (as a tarball) along with docopt

1. Create a tarball of the pip-pop code (``python setup.py sdist``)
2. Download the latest artifact from buildpacks.cloudfoundry.org (``wget https://buildpacks.cloudfoundry.org/dependencies/manual-binaries/pip-pop/pip-pop-0.1.3-fc106ef6.tar.gz``)
3. Extract the docopt tarball into the ``dist`` directory (``tar xf pip-pop-0.1.3-fc106ef6.tar.gz -C dist docopt-0.6.2.tar.gz``)
4. Create a new tarball containing the new pip-pop tarball and the docopt tarball (``tar czf pip-pop.tgz -C dist ./``)
5. Rename the file to include the version and the first 8 characters of it's sha256 (``mv pip-pop.tgz pip-pop-0.1.4-$(shasum -a256 pip-pop.tgz | cut -c1-8).tar.gz``)
