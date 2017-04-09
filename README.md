![Atom](https://cloud.githubusercontent.com/assets/72919/2874231/3af1db48-d3dd-11e3-98dc-6066f8bc766f.png)

Atom is a hackable text editor for the 21st century, built on [Electron](https://github.com/atom/electron), and based on everything we love about our favorite editors. We designed it to be deeply customizable, but still approachable using the default configuration.

Visit [atom.io](https://atom.io) to learn more or visit the [Atom forum](https://discuss.atom.io).

Follow [@AtomEditor](https://twitter.com/atomeditor) on Twitter for important
announcements.

## Building Atom 1.15.0 for armv7l machine

I unable to build the newest version of Atom due to broken mksnapshot binaries for armv7l, so in this guide we using latest stable version.

### Prerequisites

All manipulations tested on Xubuntu 14.04 @ ASUS Transformer Pad TF300TG. I don't guarantee that this guide will work for all devices. I succesfully build Atom on my machine and just want to share some build advices.

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

`script/build`

## Troubleshooting

Solving some troubles will be added tomorrow. 

## License

[MIT](https://github.com/atom/atom/blob/master/LICENSE.md)

When using the Atom or other GitHub logos, be sure to follow the [GitHub logo guidelines](https://github.com/logos).
