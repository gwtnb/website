Building Jubatus from Source
============================

We recommend using binary packages (see :doc:`quickstart`) whenever possible, but you can of course build Jubatus from source.
`jubatus-installer <https://github.com/jubatus/jubatus-installer>`_ may help your installation from source.

.. _requirements:

Requirements
------------

You need ``gcc`` (version 4.4 or later), ``pkg-config`` (version 0.26 or later) and ``python`` (version 2.6 or later, used in ``waf``) to build Jubatus from source.
In addition, following libraries are required.
For supported version of libraries, refer to the `Jubatus Wiki <https://github.com/jubatus/jubatus/wiki/Supported-Library-Versions>`_.

=================== ========== ========= ======================================================
Software            Version    Mandatory Note
=================== ========== ========= ======================================================
msgpack             >= 0.5.7   ✔
jubatus-mpio        0.4.1      ✔
jubatus-msgpack-rpc 0.4.1      ✔         C++ client library must be installed.
pficommon           master     ✔
google-glog         >= 0.3.3   ✔
mecab               >= 0.99              Required when configured with ``--enable-mecab``.
re2                 master               Required when configured *without* ``--disable-re2``
ux-trie             master               Required when configured with ``--enable-ux``.
zookeeper           >= 3.3               Required when configured with ``--enable-zookeeper``.
                                         C client library must be installed.
=================== ========== ========= ======================================================

Depending on your distribution, some libraries may be available as a binary package.
When binary packages are not available, you also need to build these libraries from source; download them from each website (
`msgpack <http://msgpack.org/>`_,
`jubatus-mpio <https://github.com/jubatus/jubatus-mpio>`_,
`jubatus-msgpack-rpc <https://github.com/jubatus/jubatus-msgpack-rpc>`_,
`pficommon <https://github.com/pfi/pficommon>`_,
`google-glog <http://code.google.com/p/google-glog/>`_,
`mecab <http://code.google.com/p/mecab/>`_,
`re2 <http://code.google.com/p/re2/>`_,
`ux-trie <http://code.google.com/p/ux-trie/>`_,
`zookeeper <http://zookeeper.apache.org/>`_
).

Ubuntu 12.04
~~~~~~~~~~~~

Here's an example on Ubuntu 12.04 systems.

::

  $ sudo apt-get install build-essential git-core pkg-config

  $ sudo apt-get install libmsgpack-dev

  $ wget http://download.jubat.us/files/source/jubatus_mpio/jubatus_mpio-0.4.1.tar.gz
  $ tar xzf jubatus_mpio-0.4.1.tar.gz
  $ cd jubatus_mpio-0.4.1
  $ ./configure
  $ make
  $ sudo make install
  $ cd ..

  $ wget http://download.jubat.us/files/source/jubatus_msgpack-rpc/jubatus_msgpack-rpc-0.4.1.tar.gz
  $ tar xzf jubatus_msgpack-rpc-0.4.1.tar.gz
  $ cd jubatus_msgpack-rpc-0.4.1
  $ ./configure
  $ make
  $ sudo make install
  $ cd ..

  $ wget -O pficommon-master.tar.gz https://github.com/pfi/pficommon/archive/master.tar.gz
  $ tar xzf pficommon-master.tar.gz
  $ cd pficommon-master
  $ ./waf configure
  $ ./waf build
  $ sudo ./waf install
  $ cd ..

  $ wget http://google-glog.googlecode.com/files/glog-0.3.3.tar.gz
  $ tar xzf glog-0.3.3.tar.gz
  $ cd glog-0.3.3
  $ ./configure
  $ make
  $ sudo make install
  $ cd ..

Now build Jubatus.

::

  $ wget -O jubatus-master.tar.gz https://github.com/jubatus/jubatus/archive/master.tar.gz
  $ tar xzf jubatus-master.tar.gz
  $ cd jubatus-master
  $ ./waf configure --disable-re2
  $ ./waf build
  $ sudo ./waf install
  $ sudo ldconfig

As this is a minimal configuration (see ``./waf configure --help`` for other configuration options available), some features like distributed mode and feature extraction plugins are not available.

Mac OS X
~~~~~~~~

We experimentally support building and running standalone mode on Mac OS X.

You can use `Homebrew tap repository <https://github.com/jubatus/homebrew-jubatus>`_ for quick installation.

Other Environments
~~~~~~~~~~~~~~~~~~

- Debian GNU/Linux runs all mode.
- Arch Linux runs standalone mode.
- FreeBSD does not run, needs some fixed on pficommon.
- We are waiting for report in other \*BSD systems and in Solaris.
