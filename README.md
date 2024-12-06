# Tailored builds for wine
Downloads available on the [releases page](https://github.com/sil-car/wine-builds/releases).

These builds are tailored for use with certain productivity-oriented software produced or used by [SIL Global](https://sil.org).
That means that many parts are left out that might be necessary for playing games but are of no use for productivity-oriented software.
The builds use the currently experimental "Shared WoW64 mode", as described on the Wine wiki's [Building Wine page](https://gitlab.winehq.org/wine/wine/-/wikis/Building-Wine#shared-wow64).

## Build parameters
Full details can be gleaned from [build-wine.yml](/.github/workflows/build-wine.yml).

### Environment variables
```
CC="gcc-9"
CXX="g++-9"
LDFLAGS: "-Wl,-O1,--sort-common,--as-needed"
```

#### 32-bit parts
```
CROSSCC="i686-w64-mingw32-gcc"
CROSSCXX="i686-w64-mingw32-g++"
CFLAGS="-march=x86-64 -msse2 -mfpmath=sse -O2 -ftree-vectorize"
PKG_CONFIG_PATH: "/usr/lib/x86_64-linux-gnu/pkgconfig"
```

#### 64-bit parts
```
CROSSCC="x86_64-w64-mingw32-gcc"
CROSSCXX="x86_64-w64-mingw32-g++"
CFLAGS="-march=x86-64 -msse3 -mfpmath=sse -O2 -ftree-vectorize"
```

### Configure options
```
--without-capi
--without-coreaudio
--without-gphoto
--without-gssapi
--without-inotify
--without-krb5
--without-oss
--without-pcap
--without-pcsclite
--without-sane
--disable-winemenubuilder
--disable-win16
--disable-tests
--enable-archs=i386,x86_64
```
