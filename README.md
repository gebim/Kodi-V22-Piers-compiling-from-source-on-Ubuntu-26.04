# Kodi V22 "Piers" compiling from source on Ubuntu 26.04

Quick write-up. Many more details can be found in the official documentation. 



### Get the source code of Kodi V22

Create a directory for the source code and the build:

 `m̀kdir kodi_V22` and `cd` into it.

Get the source:

`git clone -b Piers https://github.com/xbmc/xbmc kodi`

and you'll find the source code in the `kodi` directory.

### Install the dependencies:

``sudo apt install autoconf automake autopoint autotools-dev cmake curl debhelper default-jre doxygen gawk gcc gdc gettext gperf libasound2-dev libass-dev libavahi-client-dev libavahi-common-dev libbluetooth-dev libbluray-dev libbz2-dev libcdio-dev libcrossguid-dev libcurl4-openssl-dev libcwiid-dev libdbus-1-dev libdrm-dev libegl1-mesa-dev libenca-dev libexiv2-dev libflac-dev libfmt-dev libfontconfig-dev libfreetype6-dev libfribidi-dev libfstrcmp-dev libgcrypt-dev libgif-dev libgl1-mesa-dev libgles2-mesa-dev libglu1-mesa-dev libgnutls28-dev libgpg-error-dev libgtest-dev libiso9660-dev libjpeg-dev liblcms2-dev libltdl-dev liblzo2-dev libmicrohttpd-dev libmysqlclient-dev libnfs-dev libogg-dev libpcre2-dev libplist-dev libpng-dev libpulse-dev libshairplay-dev libsmbclient-dev libspdlog-dev libsqlite3-dev libssl-dev libtag1-dev libtiff5-dev libtinyxml-dev libtinyxml2-dev libtool libudev-dev libunistring-dev libva-dev libvdpau-dev libvorbis-dev libxmu-dev libxrandr-dev libxslt1-dev libxt-dev lsb-release meson nasm ninja-build nlohmann-json3-dev python3-dev python3-pil python3-pip swig unzip uuid-dev zip zlib1g-dev libglew-dev libwayland-dev libxkbcommon-dev waylandpp-dev wayland-protocols bison libdav1d-dev``

### Build Kodi

Create a build directory in `kodi_V22`. Must be outside the kodi source tree i.e. in `kodi_V22`:

 `mkdir kodi-build` and `cd` into it.

Configuration for Wayland:

``cmake ../kodi -DCMAKE_INSTALL_PREFIX=/usr/local -DCORE_PLATFORM_NAME=wayland -DAPP_RENDER_SYSTEM=gl -DENABLE_INTERNAL_FFMPEG=ON -DENABLE_INTERNAL_SWIG=ON -DENABLE_INTERNAL_FLATBUFFERS=ON``

Build it:

`cmake --build . -- VERBOSE=1 -j$(getconf _NPROCESSORS_ONLN)`

and if everything goes well, we'll get `kodi-wayland` binary. 

### Build the binary addons

`cd` into the `kodi` source directory. 

Let's build all binary addons. This will take quite some time, and they will be installed in `/usr/local`

`sudo make -j$(getconf _NPROCESSORS_ONLN) -C tools/depends/target/binary-addons PREFIX=/usr/local`

### Kodi installation

`cd` into `kodi-build` and do a `sudo make install`. 

Enoy this great SW.
