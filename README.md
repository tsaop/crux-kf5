# CRUX ports for KF5

As of now, this consists of the base KF5 Frameworks libraries, Plasma and a few ported applications I use daily

## Requirements

Before proceeding further, make sure your version of Qt5 is getting compiled with QtWebKit support, or you won't be able to build some packages.
Also make sure the `git` package is installed, or you won't be able to clone the repository.

## Installation

Make sure you have enabled the contrib repository, as some packages depend on it.
In `/etc/ports`, rename the file `contrib.rsync.inactive` into `contrib.rsync`:

    mv contrib.rsync.inactive contrib.rsync

Remember to also notice prt-get of the newly added repository. Edit `/etc/prt-get.conf`, uncommenting the line `#prtdir /usr/ports/contrib`:

Now update your ports tree and your system:

    ports -u
    prt-get sysup

Once that is done, you're ready to add the kf5 repo. Download the `kf5.git` file into `/etc/ports`:

    cd /etc/ports
    wget https://raw.githubusercontent.com/tsaop/crux-kf5/master/kf5.git

Update the ports tree again with `ports -u`

As before, notify prt-get of the new repo, by adding the line `prtdir /usr/ports/kf5` **before** every other port directory.

You can now install KF5 by typing:

    prt-get depinst frameworks-meta plasma-meta applications-meta --install-scripts

For your convenience I've made three metapackages respectively for frameworks libraries, plasma desktop and applications.

Please note that only a handful of KF5 applications are packaged. More will follow.

## Running

Once everything is compiled, you can now try to start your fresh KF5 environment.

Add dbus to the `SERVICES` array in `/etc/rc.conf`:

    SERVICES=(lo crond dbus [...]) 

After that, login as a regular user and edit your `.xinitrc` as follows:

    ck-launch-session dbus-launch startkde

Finally, launch Xorg with `startx` and hopefully you should be presented with a Breeze themed splash screen and, ultimately, the Plasma Desktop.
