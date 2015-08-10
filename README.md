# cross-makefiles

**cross-makefiles** is an attempt to provide the means to compile [libretro](http://www.libretro.com/) cores to as many platforms as possible, using a Linux distro as the primary building evironment.

# Details

It works by providing one `Makefile` per target platform. Those makefiles work by setting up the building toolchain (CC, CXX etc), including `Makefile.common` which builds the list of source code files to be compiled, and including `Makefile.rules` which contains the rules to make the final product.

The makefiles are generated by the `mkmake.lua` [Lua](http://www.lua.org/) script, and are provided here to help people lacking a Lua interpreter to use them.

The list of host/target platforms supported are:

* `Makefile.android-*`: builds android binaries for each one of the [supported ABIs](https://developer.android.com/ndk/guides/abis.html) from Linux, Windows and OSX hosts. The host platform is auto-detected.
* `Makefile.linux-*`: builds Linux binaries from a Linux host.
* `Makefile.linux_portable-*`: builds Linux binaries from a Linux host. The difference from these makefiles to the `linux-*` ones is that the later use `-Wl,-no-undefined` when linking the shared object.
* `Makefile.mingw*`: builds Windows binaries from a Windows host.
* `Makefile.wii`: builds Wii binaries from Linux, Windows and OSX hosts.
* `Makefile.windows-*`: builds Windows binaries from a Linux host.

Building for Android devices needs the [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html). Specify the path to the NDK by building with `NDK_ROOT_DIR=<path> make -f Makefile.android-<abi>`.

Building for Windows from a Windows host needs the `mingw-64` package to be installed. Building for the Wii needs the [devkitPPC](http://wiibrew.org/wiki/DevkitPPC). Specify the path to it by building with `DEVKITPPC_ROOT_DIR=<path> make -f Makefile.android-wii`.

## Usage

For usage examples, see [81-libretro](https://github.com/libretro/81-libretro). Specifically, the makefiles should be saved in the `build` folder under the core root folder.
