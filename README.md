# This repository is no more maintained
I no more have an armv7l device, so I can't support this project anymore.


![Atom](https://cloud.githubusercontent.com/assets/72919/2874231/3af1db48-d3dd-11e3-98dc-6066f8bc766f.png)

Atom is a hackable text editor for the 21st century, built on [Electron](https://github.com/atom/electron), and based on everything we love about our favorite editors. We designed it to be deeply customizable, but still approachable using the default configuration.

Visit [atom.io](https://atom.io) to learn more or visit the [Atom forum](https://discuss.atom.io).

Follow [@AtomEditor](https://twitter.com/atomeditor) on Twitter for important
announcements.

## Building Atom 1.15.0 for armv7l machine

![atom-1.15.0-armv7l](https://i.gyazo.com/ce02f284e5d47e0b77a60728aadf0e98.png)
I was unable to build the newest version of Atom due to broken mksnapshot binaries for armv7l, so in this guide we will be using the latest stable version (1.15.0).

This was made only for armv7l machines, and should only be built on it!

All builds tested on Xubuntu 14.04 @ ASUS Transformer Pad TF300TG. I don't guarantee that this guide will work for all devices. I have succesfully built Atom on my machine and just want to share some build advice.

### Prerequisites

- armv7l machine. You can check it by typing `uname -m` to terminal emulator.

- Node.js 6.10.2. Highly recommended to install it via [Node.js version manager](https://www.npmjs.com/). Installation guide can be found [here](https://github.com/creationix/nvm#install-script).

`nvm install 6.10.2` - install Node.js 6.10.2.

`nvm alias default 6.10.2` - set Node.js 6.10.2 as system default Node.js version.

`nvm use 6.10.2` - set Node.js version to 6.10.2 for this session.

- Node.js package manager.

`sudo apt-get install npm` - install Node.js package manager.

`sudo npm install -g npm` - update Node.js package manager.

`npm config set python /usr/bin/python2` - locate Python 2 path for Node-GYP.

- Git.

`sudo apt-get install git`

- C++ 11 Toolchain, development headers for GNOME Keyring, and other build tools.

`sudo apt-get install build-essential git libgnome-keyring-dev fakeroot rpm libx11-dev libxkbfile-dev`

### Building

- Clone my Atom fork via Git:

`git clone https://github.com/hypersad/atom-armv7l.git`

- Go into your Atom repository folder:

`cd atom-armv7l`

- Start building:

`node script/build`

- Install packages after successfull building:

`chmod a+x atom.firstboot.sh`

`./atom.firstboot.sh`

Also, you can install Atom directly, or create a Debian package.

`node script/build --create-debian-package` - creates debian package.

`sudo dpkg -i atom-armhf.deb` - installs Atom from previously built debian package (this is necessary since the `-install` flag is not supported as of now)

## Troubleshooting

- After building and launching Atom I see a white screen, developer tools and string input where I can type. Where is the interface?

It looks like Atom packages that are normally downloaded during the install are missing. You will need to launch Atom once, to let it create the profile folder (~/.atom), close it again and then run ./atom.firstboot.sh from the git repository.

- When I launch Atom, I launches succesfully, but the `tree-view` package throws an error on startup and doesn't launch. How to fix this and have `tree-view` package load correctly?

Newer versions of the `tree-view` package only work with the newer versions of Atom. Our Atom version (1.15.0) works only with tree-view 0.214.1 (this version will be installed after executing atom.firstboot.sh). So you can only run into troubles with it if you updated the `tree-view` package manually. To get the `tree-view` package working again, open terminal in your atom binaries directory (e.g if you just now compiled it `cd ~/atom-armv7l/out/atom-1.15.0-armv7l/`) and enter the following commands in terminal: `./resources/app/apm/bin/apm uninstall tree-view` wait for it to successfully uninstall, then `./resources/app/apm/bin/apm install tree-view@0.214.1`.

- After "Wrote dependencies fingerprint" I receive the following error: `Error: Cannot find module '../build/Release/runas.node'`

Runas was installed incorrectly. You need to remove it and start building again. Open your git repository folder in teminal and complete the following commands:

`sudo rm -r node_modules/runas`

`sudo rm -r lib/node_modules/runas`

Then start building again:

`node script/build`

## F.A.Q.

- Q: Can I built this fork on ia32, 64, arm, my cat, etc.?

A: No, you can't. This fork is ONLY for armv7l machines. If you want to build for any other architectures, use the official atom repo.

- Q: Do I need to avoid package updates?

A: No, you don't. You can freely update all packages, **with the exception of the `tree-view` package**, because newer versions work only with the newer versions of Atom. Our version of Atom (1.15.0) works only with `tree-view` package 0.214.1. This version installed by atom.firstboot.sh.

- Q: Do i need to execute or edit something after building?

A: You need to execute Atom binary to let it create the folder that contains configs, packages, etc. (~/.atom/), close it, then run atom.firstboot.sh to install default packages (for unknown reasons packages installed during build are missing). After package install you can freely using Atom.

## License

[MIT](https://github.com/atom/atom/blob/master/LICENSE.md)

When using the Atom or other GitHub logos, be sure to follow the [GitHub logo guidelines](https://github.com/logos).
