.. _get_nav:

How to get NavCoin Core
=======================

Get static binaries
-------------------

Final versions are released on `GitHub <https://github.com/navcoin/navcoin-core/releases>`_.

Nightly builds of the master branch are available on `build.nav.community/binaries/master <https://build.nav.community/binaries/master>`_.

Pull requests are automatically built and made available in the parent folder `build.nav.community/binaries <https://build.nav.community/binaries>`_.

Static binaries for Windows, MacOS, Linux, ARM and AARCH64 are provided. Since they are static, they can be used without any additional prerequisites.

Build from sources
------------------

Using the build script
----------------------

The easiest method to build from the source code is using the `setup.sh <https://index.nav.community/setup.sh>`_ script. The only requirement is to run it on Ubuntu 20.x.::

   curl -s https://index.nav.community/setup.sh|sudo bash -s -

This script will build an instance of the current master branch, set up the system service and will also install an instance of the electrum server.

The recommended minimum specs are a 2 core CPU and 4 GB of RAM.

The installation of the electrum server can be disable indicating the parameter ``--with_electrum 0``::

   curl -s https://index.nav.community/setup.sh|sudo bash -s - --with_electrum 0 

Install dependencies and building
---------------------------------

.. note::

   Some of the dependencies require CMake 3.14 or higher. Ubuntu 18.04 ships an older version of CMake, hence requiring to manually upgrade to a newer version. This can be done using the `Kitware APT Repository <https://apt.kitware.com>`_.

Alternatively, one can reproduce the build itself. From a fresh Linux system, one would install the dependencies and build as follows::

   sudo apt -y install build-essential libtool autotools-dev automake pkg-config git cmake libattr1-dev python3-dev
   git clone https://github.com/navcoin/navcoin-core.git
   cd navcoin-core
   git checkout master
   git pull
   cd depends
   make -j$(nproc)
   cd ..
   ./autogen.sh
   ./configure --prefix=`pwd`/depends/`uname -m`-pc-linux-gnu 
   make -j$(nproc)

The binaries will be created in the ``src`` folder.

Deterministic build using Gitian
--------------------------------

It is possible to build for any architecture using Gitian on Ubuntu 18.04 LTS Bionic Beaver::

   sudo apt update
   sudo apt install apt-transport-https ca-certificates curl software-properties-common apt-cacher
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
   sudo apt update
   sudo apt install docker-ce build-essential ruby-full apt-cacher-ng
   echo 'PassThroughPattern: .*' | sudo tee -a /etc/apt-cacher-ng/acng.conf
   sudo service apt-cacher-ng restart
   cd $HOME
   git clone https://github.com/aguycalled/gitian-builder.git
   pushd ./gitian-builder
   bin/make-base-vm --docker --arch amd64 --suite bionic
   mkdir -p inputs
   pushd ./inputs
   wget https://bitcoincore.org/cfields/osslsigncode-Backports-to-1.7.1.patch
   wget http://downloads.sourceforge.net/project/osslsigncode/osslsigncode/osslsigncode-1.7.1.tar.gz
   wget https://bitcoincore.org/depends-sources/sdks/MacOSX10.11.sdk.tar.gz
   wget https://bitcoincore.org/depends-sources/sdks/MacOSX10.14.sdk.tar.gz

In order to create the binaries, the following sequence of commands must be executed. Please, adjust ``MEMORY``, ``JOBS``, ``REPO``, ``BRANCH`` and ``OS`` as needed. ``OS`` can be ``osx``, ``win`` or ``linux``. ``linux`` includes ``ARM`` and ``AARCH64`` binaries::

   JOBS=2
   MEMORY=2000
   export REPO=navcoin
   export BRANCH=master
   export OS=linux
   rm -rf ~/navcoin-core ; cd ~ && git clone https://github.com/${REPO}/navcoin-core --branch ${BRANCH}
   cd ~/navcoin-core && git pull ; git checkout ${BRANCH} ; git pull
   cd ~/gitian-builder &&\
   USE_DOCKER=1 ./bin/gbuild --allow-sudo --memory ${MEMORY} -j${JOBS} --commit navcoin-core=${BRANCH} --url navcoin-core=${URL} ../navcoin-core/contrib/gitian-descriptors/gitian-${OS}.yml;

The compiled binaries will be found in ``~/gitian-builder/build/out``.
