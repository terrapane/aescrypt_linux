# AES Crypt Linux GUI Repository

This project contains the AES Crypt Graphical User Interface (GUI) package
for Linux.  This repository exists primary for the purpose of building
the package for installation on Linux by creating an .rpm and .deb package
file.

## Building the package

To build a release build on Linux or Mac, change directories to the root of the
source directory and issue these commands:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel
```

Then change directories to the `build` directory and issue this command:

```bash
cpack
```

This will create the `.rpm` and `.deb` files.  It will also create a `.tgz`
file, which is built since it's convenient to do.  Some users may prefer
this version to do a manual installation.

## Signed release packages

Official releases will be signed with the following GnuPG key (file named
`terrapane.asc`):

```text
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEZnioyRYJKwYBBAHaRw8BAQdARBag3n5ehV9WizHVuzS+vbAikwVQfseWlVhz
x/YBkNO0KVRlcnJhcGFuZSBTdXBwb3J0IDxzdXBwb3J0QHRlcnJhcGFuZS5jb20+
iJMEExYKADsWIQTCZNwPHBOkuxjKrxvnvpgrzVDd9AUCZnioyQIbAwULCQgHAgIi
AgYVCgkICwIEFgIDAQIeBwIXgAAKCRDnvpgrzVDd9DiGAP9lfUbSiFYx/yj3X246
/i0uUP0taN5dxx3wKRbrI05adwEApiEr/hktNmFy2laYGNwzK++UhSaQ7FrrHENx
zQoBNQO4OARmeKjJEgorBgEEAZdVAQUBAQdAjawPXr/wvH7oBykiDV5/tYVW+aTX
lLZB91r0dOQnuykDAQgHiHgEGBYKACAWIQTCZNwPHBOkuxjKrxvnvpgrzVDd9AUC
ZnioyQIbDAAKCRDnvpgrzVDd9NfgAP9GlHIUYeFpbCa2hphhRtMf4LJhaMvX5tTG
mgR/DTn4KQEA7e9z4g5RqfBZiVcPkBAZK1Y8wteMO16EgNUWvFPBMQM=
=nJuJ
-----END PGP PUBLIC KEY BLOCK-----
```

These commands are used to sign packages:

```bash
rpmsign --key-id=E7BE982BCD50DDF4 --addsign aescrypt_gui-4.0.0-Linux.rpm
debsigs --sign=origin --default-key E7BE982BCD50DDF4 aescrypt_gui-4.0.0-Linux.deb
```

The filenames for the packages will differ based on the actual version of
the file.

## Verifying the signature

This is entirely optional, but may be used to verify official packages.

### Fedora

Import the Terrapane public key like this (only needs to be done once):

```bash
rpm --import terrapane.asc
```

RPM files can then be verified like this:

```bash
rpm -K aescrypt_gui-4.0.0-Linux.rpm
```

Where the filename after `-K` will be the name of the RPM file.

### Ubuntu (and other Debian releases)

#### Setting up the policy and key ring

This only needs to be done once.

Under Ubuntu (Debian), place this file in
/etc/debsig/policies/E7BE982BCD50DDF4/debsig.pol.

```xml
<?xml version="1.0"?>
<!DOCTYPE Policy SYSTEM "https://www.debian.org/debsig/1.0/policy.dtd">
<Policy xmlns="https://www.debian.org/debsig/1.0/">
  <Origin Name="Terrapane" Description="Terrapane Group, Inc." id="E7BE982BCD50DDF4"/>
  <Selection>
    <Required Type="origin" File="debsig.gpg" id="E7BE982BCD50DDF4"/>
  </Selection>
  <Verification MinOptional="0">
    <Required Type="origin" File="debsig.gpg" id="E7BE982BCD50DDF4"/>
  </Verification>
</Policy>
```

As an aside, on Ubuntu the above policy syntax is described in the file
/usr/share/doc/debsig-verify/policy-syntax.txt.

One must also place a binary version of the Terrapane public key in the file
/usr/share/debsig/keyrings/E7BE982BCD50DDF4/debsig.gpg.  To do that, issue
these commands as root:

```bash
mkdir -p /usr/share/debsig/keyrings/E7BE982BCD50DDF4
gpg --dearmor <terrapane.asc >/usr/share/debsig/keyrings/E7BE982BCD50DDF4/debsig.gpg
```

The imported public key (`terrapane.asc`) is the one mentioned in the previous
section.

#### Verifying Debian files

Once the policies and keyring is created, verification is done using this
command:

```bash
debsig-verify aescrypt_gui-4.0.0-Linux.deb
```

## Hashed package files

Package files will also be hashed and the hash values published on the
[AES Crypt](https://www.aescrypt.com/) site.  The hash file will also be
digitally signed with the key shown above.

To compute the hash of a file, issue this command (modifying the command
according to file for which you want to compute a hash):

```bash
sha256sum aescrypt_gui-4.0.0-Linux.rpm
```

The output of that command should match the hash in the published hashes file.
