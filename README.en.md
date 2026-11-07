# Mozc-UT for Void Linux

This repository contains the template and related files required to build and package Mozc-UT for Void Linux.

It provides the build environment and related files only. Prebuilt XBPS packages are not distributed.

## Overview

- Based on the official Mozc package for Void Linux.
- Builds Mozc with integrated UT dictionaries.
- Generates packages that can be installed using XBPS.

## Features

- Integration of UT dictionary sources
- Dictionary deduplication and cost adjustment
- Offline dictionary generation
- Build and installation support for Void Linux

## Package structure

- `template`: Mozc-UT package definition
- `template.org`: Original Void Linux official Mozc template
- `update`: Package update script
- `files/`: Dictionary generation scripts and related files
- `patches/`: Patches for the build and installation environment
- `NOTICE.md`: Information about external sources and licenses
- `LICENSES/`: Full license texts

## Build and install

### 1. Get void-packages

Clone the official Void Linux `void-packages` repository.

```bash
git clone https://github.com/void-linux/void-packages.git
cd void-packages
```

### 2. Get Mozc-UT

Clone the Mozc-UT repository into `srcpkgs/mozc-ut`.

```bash
git clone https://github.com/linakichi/void-packages-mozc-ut.git srcpkgs/mozc-ut
```

`srcpkgs/mozc-ut` is an independent Git repository. Update it separately from the Git repository for `void-packages`.

### 3. Create symbolic links

Create the links required for the Mozc-UT subpackages.

```bash
ln -s mozc-ut srcpkgs/mozc-ut-base
ln -s mozc-ut srcpkgs/ibus-mozc-ut
ln -s mozc-ut srcpkgs/fcitx5-mozc-ut
```

### 4. Initialize the build environment

This is performed automatically during the first build. To initialize the build environment explicitly, run:

```bash
./xbps-src binary-bootstrap
```

### 5. Build Mozc-UT

```bash
./xbps-src pkg mozc-ut
```

The resulting packages are normally placed in `hostdir/binpkgs`.

`xbps-src` automatically fetches and configures the required build dependencies based on the declarations in the package template. However, the versions of dependencies and build tools depend on the state of the `void-packages` repository and the repositories being used.

The first build downloads the UT dictionaries and builds Mozc itself. On the ThinkPad E490 used for testing, dictionary downloads took approximately 10 minutes, and package building took approximately 20 minutes. Actual times vary depending on the environment and cache state.

### 6. Remove existing Mozc packages

Mozc-UT conflicts with the standard Mozc packages. Remove any existing Mozc-related packages before installation.

```bash
sudo xbps-remove mozc mozc-base ibus-mozc fcitx5-mozc
```

If some of these packages are not installed, omit their names from the command.

### 7. Install Mozc-UT

Run one of the following commands depending on which input method framework you use.

**Fcitx5**

```bash
sudo xbps-install --repository=hostdir/binpkgs \
  mozc-ut-base mozc-ut fcitx5-mozc-ut
```

**IBus**

```bash
sudo xbps-install --repository=hostdir/binpkgs \
  mozc-ut-base mozc-ut ibus-mozc-ut
```

## Notes

- Run `xbps-src` as a regular user, not as root.
- The Mozc version used for the build is specified in this repository's `template`.
- Build dependencies depend on the state of the `void-packages` repository and the repositories being used.
- Updates to the official Void Linux packages may change the build environment or dependencies and could cause the build to fail.
- Verify that the build completes successfully before installing the packages.
- Mozc-UT conflicts with the standard Mozc packages. Remove existing packages before installation.

## Dictionary sources

The following UT dictionary sources are currently integrated by the `template`.

| Dictionary source | Description |
|---|---|
| jawiki | Dictionary derived from the Japanese Wikipedia |
| neologd | mecab-ipadic-neologd |
| personal | Personal names dictionary |
| place | Place names dictionary |
| sudachi | Sudachi dictionary |

For details about source locations, versions, licenses, and other information, see `NOTICE.md`.

The dictionary composition may change in future updates.

## Updating

### Updating void-packages

Run the following command from the `void-packages` directory to pull updates from the official repository.

```bash
git pull
```

If necessary, update the bootstrap packages used by the build environment as well.

```bash
./xbps-src bootstrap-update
```

After updating, verify that Mozc-UT still builds successfully.

```bash
./xbps-src pkg mozc-ut
```

### Updating Mozc-UT

The Mozc-UT repository is independent of `void-packages` and must be updated separately.

```bash
git -C srcpkgs/mozc-ut pull
```

After updating, verify that the build completes successfully again.

## License

This project includes code and dictionary data distributed under different licenses.

Please respect the licenses and copyright notices applicable to each file and data source. See `NOTICE.md` and `LICENSES/` for details.
