## Ports for constructing the 'lxqt' and 'lxqt-extra' collections

Contributions are welcome. If you don't know what it all about, please take the time to read the documentation at
http://www.nutyx.org/en/build-package.html
(version française)
http://www.nutyx.org/fr/build-package.html

It will explain you what's a collection, a git, a port, the tools around 'cards' etc

### How to test this git:

#### 1. Clone it in your home directory

    $ cd
    $ git clone git://github.com/NuTyX/lxqt.git
    $ git clone git://github.com/NuTyX/core.git

#### 2. Become root until the end, define and create the directory used by the scripts:

 The script is checking the files /etc/install-nutyx.conf and /etc/install-nutyx.conf.d/cards.conf if they exist, if yes it will use them, so:

    $ su -
    # echo "LFS=/mnt/lfs
    DEPOT=/DEPOT" > /etc/install-nutyx.conf
    # mkdir -p /etc/install-nutyx.conf.d
    # cat > /etc/install-nutyx.conf.d/cards.conf << "EOF"
    dir /DEPOT/lxqt
    dir /DEPOT/gui
    dir /DEPOT/cli
    dir /DEPOT/base|http://downloads.nutyx.org
    dir /DEPOT/base-extra|http://downloads.nutyx.org
    base /DEPOT/base
    base /DEPOT/base-extra
    logdir /var/log/pkgbuild
    EOF

#### 3. Install a base NuTyX system (assume below the user is 'tnut' so adapt to yours)

    # bash /home/tnut/core/scripts/install-nutyx

#### 4. In your chroot Make the directory where the git copy will comes

    # mkdir -v /mnt/lfs/root/{core,lxqt}

#### 5. Mount your git project (assume below the user is 'tnut' so adapt to yours)

    # mount -o bind /home/tnut/lxqt /mnt/lfs/root/lxqt
    # mount -o bind /home/tnut/core /mnt/lfs/root/core

#### 6. Enter now in your chroot

    # bash /home/tnut/core/scripts/install-nutyx -ec

#### 7. Prepare the first execution of the build script

    # get cards.devel git
 
#### 8. If everything is OK, synchronize the  core 'base', 'cli' and 'gui' collections binaries

    # cd /root/core
    # bash scripts/base -s
    # bash scripts/cli -s
    # bash scripts/gui -s
    
#### 9. If everything is OK, synchronize the 'lxqt' collection binaries 

    # cd /root/lxqt
    # bash scripts/lxqt -s

#### 10. If everything is OK, check with cards level what's new

    # cards level

 It should shows all the packages available.

#### 11. If you want to build the 'lxqt' collection from the sources

    # bash scripts/lxqt -a

#### 12. If you want to build the 'lxqt-extra' collection from the sources, add the proper line in top of the cards.conf file like this:

    dir /core/lxqt-extra

 then you are ready to compile the 'lxqt-extra' collection

    # cd /root/lxqt
    # bash scripts/lxqt-extra -s
    # bash scripts/lxqt-extra -a 

Have fun :)
