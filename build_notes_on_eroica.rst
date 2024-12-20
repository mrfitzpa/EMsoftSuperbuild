Build notes on work laptop
==========================

Installing latest cmake
-----------------------

First, run the following commands::

  sudo apt remove --purge --auto-remove cmake

  sudo apt update
  sudo apt install -y software-properties-common lsb-release
  sudo apt clean all

  wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | sudo tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null

  sudo apt-add-repository "deb https://apt.kitware.com/ubuntu/ $(lsb_release -cs) main"

  sudo apt update
  sudo apt install kitware-archive-keyring
  sudo rm /etc/apt/trusted.gpg.d/kitware.gpg

If ``sudo apt update`` yields the following error::

  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY <PUBLIC-KEY>

where ``<PUBLIC-KEY>`` is a public key (e.g. ``1A127079A92F09ED``), copy the
public key and run::

  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1A127079A92F09ED

Finally, run::

  sudo apt update
  sudo apt install cmake

Installing gcc
--------------

Run::

  sudo apt update
  sudo apt install build-essential

Installing clang
----------------

Run::

  sudo apt update
  sudo apt install clang

Installing gfortran
-------------------

Run::

  sudo apt update
  sudo apt install gfortran

Building the SDK
----------------

Run::

  cd EMsoftSuperbuild
  mkdir Debug
  cd Debug
  sudo cmake -DEMsoft_SDK=/opt/EMsoft/EMsoft_SDK -DCMAKE_BUILD_TYPE=Debug ../
  sudo make -j
  cd ../
  mkdir Release
  cd Release
  sudo cmake -DEMsoft_SDK=/opt/EMsoft/EMsoft_SDK -DCMAKE_BUILD_TYPE=Release ../
  sudo make -j
