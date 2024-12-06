# Tailored builds for wine
Downloads available on the [releases page](https://github.com/sil-car/wine-builds/releases). If the minor increment of the wine version is a '0' (e.g. 9.0.1), then it's a stable build. Otherwise it's a devel branch build (e.g. 9.22). There are no builds from wine-staging at the moment. The part after the '+' represents the build base, so '+20.04' means the files were compiled on Ubuntu 20.04, which uses GLIBC v2.31, which means they should work on any other system with GLIBC v2.31 or higher.

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
