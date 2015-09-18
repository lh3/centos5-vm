[CentOS 5][centos], released on 2007-04-12, is one of the oldest Linux
distributions that are still maintained (until 2017-03-31) and remain widely
used nowadays. Due to its age, quite a few programs are hard to be compiled on
CentOS 5 caused by the lack of modern compilers and libraries; binaries
compiled on recent Linux distributions are often not working on CentOS 5 due to
ABI incompatibility in core libraries. CentOS 5 is a major obstacle to software
portability. On the bright side, because most core libraries are backward
compatible, binaries compiled on CentOS 5 without 3rd-party dynamic libraries
often work on recent Linux distributions. CentOS 5 gives a way to generate
portable executables.

This virtual repository (with no code and data) describes how to deploy CentOS
5 virtual machine (VM) on your laptop or desktop computers such as you can test
your programs on this older system and produce portable precompiled binaries.

#### Installation and Usage

1. Install [VirtualBox][vb]. The VM was created on the [version 4.3.x][vb43],
   though the latest version 5.0 may also work.

2. Install [Vagrant][vg].

3. Run the following command lines on the host system:
   ```sh
   mkdir -p $HOME/centos5; cd $HOME/centos5
   wget -O centos5.box http://sourceforge.net/projects/biobin/files/devtools/centos5.box/download
   vagrant box add centos5 centos5.box # unpack
   vagrant init                        # initialize
   vagrant up                          # launch VM
   vagrant ssh                         # ssh to VM
   ```

4. The login account is `vagrant` with password `vagrant`. It has the `sudo`
   permission. Directory `/vagrant` in the VM is identical to `$HOME/centos5`
   in the host system. You can transfer data through this shared directory.

5. Precompiled GCC-4.9.2 and Boost-1.57.0 can be [found here][biobin]. To use
   them, inside the VM:
   ```sh
   cd /opt
   wget -O- http://sourceforge.net/projects/biobin/files/devtools/gcc-static-4.9.2_x64-centos5.tar.bz2/download \
     | sudo tar -jxf -
   ls /opt/devel/bin/gcc
   ```
   These binaries are compiled with dynamic libraries disabled. As a results, 
   binaries compiled with this GCC or linked against Boost will be portable to
   other systems.

[centos]: https://en.wikipedia.org/wiki/CentOS
[vb]: https://www.virtualbox.org/wiki/Downloads
[vb43]: https://www.virtualbox.org/wiki/Download_Old_Builds_4_3
[vg]: https://www.vagrantup.com/downloads.html
[biobin]: https://sourceforge.net/projects/biobin/files/devtools/
