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

## Install prerequisites

Follow the instructions for your platform:

- [macOS](https://github.com/brave/brave-browser/wiki/macOS-Development-Environment)
- [Windows](https://github.com/brave/brave-browser/wiki/Windows-Development-Environment)
- [Linux/Android](https://github.com/brave/brave-browser/wiki/Linux-Development-Environment)

## Clone and initialize the repo

Once you have the prerequisites installed, you can get the code and initialize the build environment.

```bash
git clone git@github.com:PresearchOfficial/presearch-browser-android.git
cd presearch-browser-android
npm install

# the Chromium source is downloaded, which has a large history
# this might take really long to finish

npm run init
```
presearch-browser-core based android builds should use `npm run init -- --target_os=android --target_arch=arm` (or whichever CPU type you want to build for)

You can also set the target_os and target_arch for init and build using:

```
npm config set target_os android
npm config set target_arch arm
```

## Build Presearch
The default build type is component.

```
# start the component build compile
npm run build
```

To do a release build:

```
# start the release compile
npm run build Release
```

presearch-browser-core based android builds should use `npm run build -- --target_os=android --target_arch=arm` or set the npm config variables as specified above for `init`

### Build Configurations

Running a release build with `npm run build Release` can be very slow and use a lot of RAM, especially on Linux with the Gold LLVM plugin.

To run a statically linked build (takes longer to build, but starts faster):

```bash
npm run build -- Static
```

To run a debug build (Component build with is_debug=true):

```bash
npm run build -- Debug
```

## Run Presearch
To start the build:

`npm start [Release|Component|Static|Debug]`

# Enabling third-party APIs:

1. **Google Safe Browsing**: Get an API key with SafeBrowsing API enabled from https://console.developers.google.com/. Update the `GOOGLE_API_KEY` environment variable with your key as per https://www.chromium.org/developers/how-tos/api-keys to enable Google SafeBrowsing.

# Development
- Security rules: https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/security/rules.md