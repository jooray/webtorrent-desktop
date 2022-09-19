# WebTorrent Desktop - Privacy Edition

The streaming torrent app. For Mac, Windows, and Linux.

## About this fork

This is a privacy extended version of
[webtorrent](https://webtorrent.io/), with the following
changes:

- No autoupdate mechanism. The main reason is that I do it for my
  personal purposes and I don't want to compile it for other platforms

- Automatically stop seeding after download. Yes, I know, being a leech
  is not nice. If you want to seed, you can click on the torrent again
  to seed manually. Please be nice and seed, but if you are in a hotel
  room or on a data connection, you want to stop seeding as soon as
  possible.

- Do not send anonymized telemetry to Webtorrent servers. I have nothing
  against doing it by default, but it should be configurable. This
  edition has it off by default

Please do not expect me to keep this version up to date, handle bugs nor
compile a version for your platform.

If you need to compile it for your
platform, follow the compile and packaging instructions.

## Acknowledgements to upstream WebTorrent

I would like to thank the WebTorrent team for making an amazing piece of
software, this is just a flavor that I like more. And thanks to the
open-source edition. All credit goes to the WebTorrent team for making
this possible, head over to [their website](https://webtorrent.io/) for
new version, cool new stuff and services.

## Running and installing

Or you can just do this from the command line:

```bash
npm install && npm start
```

## How to compile and package

### Get the code

```
$ git clone https://github.com/webtorrent/webtorrent-desktop.git
$ cd webtorrent-desktop
$ npm install
```

### Run the app

```
$ npm start
```

### Watch the code

Restart the app automatically every time code changes. Useful during development.

```
$ npm run watch
```

### Run linters

```
$ npm test
```

### Run integration tests

```
$ npm run test-integration
```

The integration tests use Spectron and Tape. They click through the app, taking screenshots and
comparing each one to a reference. Why screenshots?

* Ad-hoc checking makes the tests a lot more work to write
* Even diffing the whole HTML is not as thorough as screenshot diffing. For example, it wouldn't
  catch an bug where hitting ESC from a video doesn't correctly restore window size.
* Chrome's own integration tests use screenshot diffing iirc
* Small UI changes will break a few tests, but the fix is as easy as deleting the offending
  screenshots and running the tests, which will recreate them with the new look.
* The resulting Github PR will then show, pixel by pixel, the exact UI changes that were made! See
  https://github.com/blog/817-behold-image-view-modes

For MacOS, you'll need a Retina screen for the integration tests to pass. Your screen should have
the same resolution as a 2018 MacBook Pro 13".

For Windows, you'll need Windows 10 with a 1366x768 screen.

When running integration tests, keep the mouse on the edge of the screen and don't touch the mouse
or keyboard while the tests are running.

### Package the app

Builds app binaries for Mac, Linux, and Windows.

```
$ npm run package
```

To build for one platform:

```
$ npm run package -- [platform] [options]
```

Where `[platform]` is `darwin`, `linux`, `win32`, or `all` (default).

The following optional arguments are available:

- `--sign` - Sign the application (Mac, Windows)
- `--package=[type]` - Package single output type.
   - `deb` - Debian package
   - `rpm` - RedHat package
   - `zip` - Linux zip file
   - `dmg` - Mac disk image
   - `exe` - Windows installer
   - `portable` - Windows portable app
   - `all` - All platforms (default)

Note: Even with the `--package` option, the auto-update files (.nupkg for Windows,
-darwin.zip for Mac) will always be produced.

#### Windows build notes

The Windows app can be packaged from **any** platform.

Note: Windows code signing only works from **Windows**, for now.

Note: To package the Windows app from non-Windows platforms,
[Wine](https://www.winehq.org/) and [Mono](https://www.mono-project.com/) need
to be installed. For example on Mac, first install
[XQuartz](http://www.xquartz.org/), then run:

```
$ brew install wine mono
```

(Requires the [Homebrew](http://brew.sh/) package manager.)

#### Mac build notes

The Mac app can only be packaged from **macOS**.

#### Linux build notes

The Linux app can be packaged from **any** platform.

If packaging from Mac, install system dependencies with Homebrew by running:

```
npm run install-system-deps
```
#### Recommended readings to start working in the app

Electron (Framework to make native apps for Windows, OSX and Linux in Javascript):
https://electronjs.org/docs/tutorial/quick-start

React.js (Framework to work with Frontend UI):
https://reactjs.org/docs/getting-started.html

Material UI (React components that implement Google's Material Design.):
https://material-ui.com/getting-started/installation

## License

MIT. Copyright (c) [WebTorrent, LLC](https://webtorrent.io).
Privacy enhancements [Juraj Bednar](https://github.com/jooray/webtorrent-desktop).

Please note that this is not an official Webtorrent client, but a
privacy enhanced fork!
