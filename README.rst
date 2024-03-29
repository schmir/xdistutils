.. -*- mode: rst; coding: utf-8 -*-

======================================================================
xdistutils - useful distutils extensions
======================================================================

:Authors: Ralf Schmitt <ralf@systemexit.de>
:Version: 0.2.0
:Date:    2012-02-08
:Download: http://pypi.python.org/pypi/xdistutils
:Code: https://github.com/schmir/xdistutils

.. contents:: Table of Contents
  :backlinks: top


xdistutils currently provides a recompress command for python's
setup.py scripts. It uses the advancecomp_ package in order to achieve
better compression on .zip, .egg and .tar.gz files.  Other extensions
for distutils may be included in future xdistutils releases.


Installation
========================================
xdistutils can be installed with pip or easy_install. In order to
enable the recompress command, you'll have to register the package
with distutils. This can be done by adding the following to
~/.pydistutils.cfg::

  [global]
  command-packages=xdistutils

The advancecomp_ package must be installed on your system.

The recompress command
========================================
Every setup.py script now understands a recompress command, which will
call advzip or advdef on any .zip, .egg or .tar.gz file generated by
previous commands::

  > python setup.py sdist bdist_egg recompress
  running sdist
  make: Nothing to be done for `all'.
  running check
  reading manifest template 'MANIFEST.in'
  writing manifest file 'MANIFEST'
  creating gevent-1.0dev
  creating gevent-1.0dev/c-ares
  ...
  writing build/bdist.linux-x86_64/egg/EGG-INFO/native_libs.txt
  creating 'dist/gevent-1.0dev-py2.7-linux-x86_64.egg' and adding 'build/bdist.linux-x86_64/egg' to it
  removing 'build/bdist.linux-x86_64/egg' (and everything under it)
  running recompress
  advzip -z -4 dist/gevent-1.0dev.zip
       1300236     1243960  95% dist/gevent-1.0dev.zip
       1300236     1243960  95%
  advzip -z -4 dist/gevent-1.0dev-py2.7-linux-x86_64.egg
	366596      354053  96% dist/gevent-1.0dev-py2.7-linux-x86_64.egg
	366596      354053  96%

The bdist_msi_fixed command
========================================
bdist_msi is used on windows in order to create a .msi
installler. It's part of standard distutils. Though a bug_ in distutils
makes it impossible to upload those .msi files to the python package
index with the upload command. bdist_msi_fixed provides a workaround::

  > python setup.py bdist_msi_fixed
  running bdist_msi_fixed
  running bdist_msi
  ...
  > python setup.py bdist_msi_fixed upload

.. _advancecomp: http://advancemame.sourceforge.net/comp-readme.html
.. _bug: http://bugs.python.org/issue13719
