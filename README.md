![Atom](https://cloud.githubusercontent.com/assets/72919/2874231/3af1db48-d3dd-11e3-98dc-6066f8bc766f.png)

Atom is a hackable text editor for the 21st century, built on [Electron](https://github.com/atom/electron), and based on everything we love about our favorite editors. We designed it to be deeply customizable, but still approachable using the default configuration.

Visit [atom.io](https://atom.io) to learn more or visit the [Atom forum](https://discuss.atom.io).

Follow [@AtomEditor](https://twitter.com/atomeditor) on Twitter for important
announcements.

## Building Atom 1.15.0 for armv7l machine

![atom-1.15.0-armv7l](https://i.gyazo.com/ce02f284e5d47e0b77a60728aadf0e98.png)
I was unable to build the newest version of Atom due to broken mksnapshot binaries for armv7l, so in this guide we will be using the latest stable version (1.15.0).

Please, do not try to build it on other platforms. This fork only for armv7l machines!

### Prerequisites

All manipulations tested on Xubuntu 14.04 @ ASUS Transformer Pad TF300TG. I don't guarantee that this guide will work for all devices. I succesfully built Atom on my machine and just want to share some build advice.

- armv7l machine. You can check it by typing `uname -m` to terminal emulator.

- Node.js 6.10.2. Highly recommended to install it via [Node.js version manager](https://www.npmjs.com/). Installation guide can be found [here](https://github.com/creationix/nvm#install-script).

`nvm install 6.10.2` - install Node.js 6.10.2.

`nvm alias default 6.10.2` - set Node.js 6.10.2 as system default Node.js version.

`nvm use 6.10.2` - set Node.js version to 6.10.2 for this session.

- Node.js package manager 4.4.4.

`sudo apt-get install npm` - install Node.js package manager.

`npm install -g npm` - update Node.js package manager.

`npm config set python /usr/bin/python2` - locate Python 2 path for Node-GYP.

- Git.

`sudo apt-get install git`

- C++ 11 Toolchain, development headers for GNOME Keyring, and other build tools.

`sudo apt-get install build-essential git libgnome-keyring-dev fakeroot rpm libx11-dev libxkbfile-dev`

### Building

- Clone my Atom fork via Git:

`git clone https://github.com/hypersad/atom.git`

- Go into your Atom repository folder:

`cd atom`

- Start building

`node script/build`

## Troubleshooting

- After building and launching Atom I got white screen, developer tools and error in developer console says "index.js:56 Error: ENOENT, node_modules/log4js/node_modules/semver/semver.js not found in /home/%username%/atom/out/atom-1.15.0-armv7l/resources/app.asar"

Okay, I don't know how to fix this error before installing, but I have a way to fix it after: 

Open your Atom folder with sources (where you download Atom via git) - e.g `cd ~/atom/`. 

Install asar (electron archivator-like programm) by `npm install asar` and after installing go to atom/out/atom-1.15.0-armv7l/resources by `cd ~/atom/out/atom-1.15.0-armv7l/resources`.

Unpack app.asar in folder app.asar.ext (no matter how you name it) by `node ~/atom/node_modules/asar/bin/asar.js e app.asar app.asar.ext` and wait some time for extracting.

After successful extracting app.asar go into app.asar.ext (`cd app.asar.ext`) and install log4js there by typing `npm install --save-dev log4js`

After installing log4js go into it's folder (`cd node_modules/log4js`) and install semver by typing `npm install --save-dev semver`

After all this steps, backup original app.asar to somewhere, remove it and pack app.asar.ext into app.asar by following commands: `cd ~/atom/out/atom-1.15.0-armv7l/resources`; `node ~/atom/node_modules/asar/bin/asar.js p app.asar.ext app.asar` and after succesful packing try to launch Atom. If error disappeared but you still have white screen - complete the next troubleshooting part (below this).

- After building and launching Atom I got white screen, developer tools and string where I can type. Where is interface?

It looks like Atom packages that are normally downloaded during install are missing. You will need to launch Atom for first time, to let it create the profile folder (~/.atom), close Atom, then, move atom.firstboot.sh to your ready Atom folder with binaries (e.g ~/atom/app/atom-1.15.0-armv7l/) and launch it. This script will reinstall all default packages.

- When I launch Atom, I got succesfull launch, but tree-view package throw error on start and didn't launch. How to fix it and launch tree-view package?

Newer versions of tree-view package works only with the newer versions of Atom. Our Atom version (1.15.0) works only with tree-view 0.214.1 (this version will be installed after executing atom.firstboot.sh). So you can have troubles with it only if you updated tree-view package. To get working tree-view package back, open terminal in your atom binaries directory (e.g if you just now compiled it `cd ~/atom/out/atom-1.15.0-armv7l/`) and complete following commands in terminal: `./resources/app/apm/bin/apm uninstall tree-view` wait for successfull uninstal, then `./resources/app/apm/bin/apm install tree-view@0.214.1`.

## F.A.Q.

- Q: Can I built this fork on ia32, 64, arm, my cat, etc.?

A: No, you can't. This fork is ONLY for armv7l machines.

- Q: Do I need to avoid package updates?

A: No, you don't. You can freely update all packages exclude tree-view package, because newer versions works only with newer versions of Atom. Our version of Atom (1.15.0) works only with tree-view package 0.214.1. This version installed by atom.firstboot.sh.

## License

[MIT](https://github.com/atom/atom/blob/master/LICENSE.md)

When using the Atom or other GitHub logos, be sure to follow the [GitHub logo guidelines](https://github.com/logos).
