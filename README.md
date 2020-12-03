# OpenWrt Firmware Selector

A simple OpenWrt firmware selector using autocompletion. Uses plain
HTML/CSS/JavaScript. Checkout the [Demo](https://firmware-selector.openwrt.org).

![image](misc/screenshot.png)


## Quick Run

* Download the sources and change the working directory
* Start webserver (e.g. `python3 -m http.server`)
* Go to `http://localhost:8000/www/` in your web browser

Configure with [config.js](www/config.js).

## Attended Sysupgrade Support

This firmware selector can speak to a [ASU server](https://github.com/aparcar/asu) to build custom images. To enable the feature, the `asu_url` option in the config.js needs to be set.

## Installation

Place the `www/` folder somewhere web accessible. Then use the `collect.py` script to update `www/config.json` and write all device data into `www/data/`:

```
./misc/collect.py --image-url 'https://downloads.openwrt.org/{base}/{target}' https://downloads.openwrt.org  www/
```
or for local accessible OpenWrt builds:

```
./misc/collect.py --image-url 'https://downloads.openwrt.org/{base}/{target}' ~/openwrt/bin  www/
```

This should do it!

Settings `image_url` and `info_url` can also be passed to `misc/collect.py` to be included in the version specific `overview.json` files:

`--image-url`: Download link template for the image files.
`--info-url`: Link template that points to additional information.

* `{version}`: Version in the profiles.json files. E.g. `19.07.4` or `SNAPSHOT`.
* `{id}`: Device identifier. E.g. `tplink_archer-c7-v2`
* `{target}`: Main- and sub target, E.g. `ath79/generic`.
* `{base}`: Distinct path to the targets directory. E.g. `releases/18.06.8/targets/`  
  Handled by `misc/collect.py` only!

### Generate OpenWrt JSON

The collect.py script merges data from `profile.json` files generated by OpenWrt. To enable generation, go to the build settings (`make menuconfig`):
`Global build settings  ---> [*] Create JSON info files per build image`.

If the option is not available (OpenWrt 18.06 or 19.07.3), apply commit [openwrt/openwrt@881ed09](https://github.com/openwrt/openwrt/commit/881ed09ee6e23f6c224184bb7493253c4624fb9f).

## Similar Projects

- [Gluon Firmware Selector](https://github.com/freifunk-darmstadt/gluon-firmware-selector): For [Gluon](https://github.com/freifunk-gluon/) images, now with pictures.
- [Freifunk Hennef Firmware Downloader](https://github.com/Freifunk-Hennef/ffhef-fw-dl): Similar to the project above, but PHP based.
- [LibreMesh Chef](https://github.com/libremesh/chef/): Allows to select configurations.
- [GSoC Firmware Selector](https://github.com/sudhanshu16/openwrt-firmware-selector/): Result of the GSoC
- [FFB Firmware Selector](https://github.com/freifunk-bielefeld/firmware-selector): Build for Freifunk Bielefeld
