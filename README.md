# AES Crypt Linux and FreeBSD GUI Repository

This project contains the AES Crypt Graphical User Interface (GUI) package
for Linux and FreeBSD.

## Building the package

To build a release build on Linux or FreeBSD, change directories to the root of
the source directory and issue these commands:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -Daescrypt_ENABLE_LICENSE_MODULE:BOOL=OFF
cmake --build build --parallel
```

Note that while it is possible to build the software from source code,
a license is required to use AES Crypt.  Refer to the AES Crypt site
[here](https://www.aescrypt.com/license.html).

Then change directories to the `build` directory and issue this command:

```bash
cpack
```

This will create the `.rpm` and `.deb` files.  It will also create a `.tgz`
file, which is built since it's convenient to do.  Some users may prefer
this version to do a manual installation.

## Usage

One may use AES Crypt either from the Linux desktop or from the command-line.
Visit the Linux/FreeBSD [usage page](https://www.aescrypt.com/linux_aes_crypt.html)
for details about using AES Crypt for the desktop or command-line.
