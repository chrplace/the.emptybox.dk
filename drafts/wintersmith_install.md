Install Wintersmith on debian/ubuntu from latest
======


```
sudo apt-get install pkg-config build-essential python g++ make checkinstall
sudo ln -s /usr/bin/gcc /usr/bin/cc #  See note on cc missing below
src=$(mktemp -d) && cd $src
wget -N http://nodejs.org/dist/node-latest.tar.gz
tar xzvf node-latest.tar.gz && cd node-v*
./configure 
sudo checkinstall -y --install=no --pkgversion 0.10.25  make -j$(($(nproc)+1)) install
dpkg -i node_0.10.25-1_amd64.deb
sudo dpkg -i node_0.10.25-1_amd64.deb
sudo npm install -g wintersmith
```
source: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager

### Notes
* <a name="missingcc"></a>`cc` missing:  
   On debian 7 it just worked, with out doing the link for cc, but on Ubuntu 13.10 `cc` was missing

   ```
   $ ./configure 
   Node.js configure error: No acceptable C compiler found!

        Please make sure you have a C compiler installed on your system and/or
        consider adjusting the CC environment variable if you installed
        it in a non-standard prefix.
   ```
   Looking in the node configure script I investigated the `os.environ.get` call
   ```
   $ python
   Python 2.7.5+ (default, Sep 19 2013, 13:48:49) 
   [GCC 4.8.1] on linux2
   Type "help", "copyright", "credits" or "license" for more information.
   >>> import os
   >>> os.environ.get('CC', 'cc')
   'cc'
   $ cc
   The program 'cc' can be found in the following packages:
    * gcc
    * clang
    * pentium-builder
    * tcc
   Try: sudo apt-get install <selected package>
   $ sudo apt-get install gcc
   ...
   gcc is already the newest version.
   ```


