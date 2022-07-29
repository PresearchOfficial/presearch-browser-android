# Presearch Browser


## Overview

This repository holds the build tools needed to build the Presearch desktop browser for macOS, Windows, and Linux.  In particular, it fetches and syncs code from the projects defined in `package.json` and `src/presearch/DEPS`:

  - [Chromium](https://chromium.googlesource.com/chromium/src.git)
    - Fetches code via `depot_tools`.
    - sets the branch for Chromium (ex: 65.0.3325.181).
  - [presearch-core](https://github.com/PresearchOfficial/presearch-browser-core)
    - Mounted at `src/presearch`.
    - Maintains patches for 3rd party Chromium code.
  - [adblock-rust](https://github.com/brave/adblock-rust)
    - Implements Brave's ad-block engine.
    - Linked through [brave/adblock-rust-ffi](https://github.com/PresearchOfficial/presearch-browser-core/tree/master/components/adblock_rust_ffi).

## Other repositories

For other versions of our browser, please see:

* iOS - [PresearchOfficial/presearch-browser-ios](https://github.com/PresearchOfficial/presearch-browser-ios.git)

## Contributing

Please see the [contributing guidelines](./CONTRIBUTING.md).

## Community

[Join the Q&A community](https://www.presearch.io/collaborate) if you'd like to get more involved with Presearch. You can [ask for help](https://support.presearch.org/support/home).

Follow [@presearch](https://twitter.com/TeamPresearch) on Twitter for important news and announcements.

## Build for Android
### System Requirements

Before you begin, ensure your system satisfies the [system requirements](https://chromium.googlesource.com/chromium/src/+/master/docs/linux/build_instructions.md#system-requirements).
The Android build can only be made on Linux machine. The process described in this instruction uses Ubuntu 20.

### Setup build environment for Android

You will need `Git`, `Python 3`, the `Node.js` active LTS (v16+), and `npm` (v8+ but < 8.6). You may need to make `python3` the default if `Python 2.7` is default for your OS. Also, if you don't have anything named python on your machine and only have `python3`, you will need something like `python-is-python3`.

### Clone and initialize the repo

Once you have the prerequisites installed, you can get the code and initialize the build environment.

```bash
git clone https://github.com/PresearchOfficial/presearch-browser-android.git
cd presearch-browser-android
npm install

# the Chromium source is downloaded, which has a large history
# this might take really long to finish

npm run init
```

After `npm run init` is finished, there is one final step to finish installing build dependencies. This shell script only works on Debian and Ubuntu but check [system requirements](https://github.com/chromium/chromium/blob/master/docs/linux/build_instructions.md#system-requirements) for other distros:

```bash
# Run this cli into the presearch-browser-android folder
./src/build/install-build-deps-android.sh
```
### Making debug build for Android

presearch-browser-core based android builds should use `npm run init -- --target_os=android --target_arch=arm` (or whichever CPU type you want to build for)

Or set the target_os and target_arch for init and build using:

```
npm config set target_os android
npm config set target_arch arm # For 32 bits ARM
npm config set target_arch arm64 # For 64 bits ARM
```

## Build Presearch
The default build type is component.

```
# start the component build compile
npm run build
```
```
