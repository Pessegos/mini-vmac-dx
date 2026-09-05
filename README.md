# Mini vMac Plus

An unofficial quality-of-life fork of Mini vMac for modern Windows.

This repository contains source code only. It does not include Macintosh ROMs,
Mac OS disk images, games, save disks, or prebuilt executables with embedded
software.

## What This Changes

- Direct3D 9Ex renderer for smoother fullscreen presentation on modern Windows.
- Direct3D 9 fallback, with the original GDI path still available as a last resort.
- Crisp point/nearest scaling for pixel art.
- Full-monitor fullscreen toggled with Alt+Enter.
- View menu and right-click fullscreen controls.
- Resizable window with aspect-aware fit rendering.
- Window maximize behaves like a normal Windows app.
- Alt+Tab and Windows hotkeys are friendlier in fullscreen.
- Windowed mouse behavior uses click-to-capture so resizing and menus stay usable.
- DPI-aware Windows manifest.

## What Is Not Included

This repo intentionally does not include:

- Apple Macintosh ROM files.
- Mac OS/System disk images.
- Prince of Persia or any other commercial game data.
- Disk images such as `.dsk`, `.hfv`, `.hfs`, or `.iso`.
- Prebuilt private launcher executables.
- Game-derived icons or artwork.

You need to supply any ROM and disk images yourself.

## Build On Windows

Install MSYS2 and the 32-bit MinGW toolchain:

```sh
pacman -S --needed base-devel mingw-w64-i686-gcc mingw-w64-i686-make
```

Open the **MSYS2 MINGW32** shell and run:

```sh
cd /path/to/this/repo/minivmac
make
```

If your MSYS2 install provides `mingw32-make`, that also works.

The output is:

```text
minivmac-plus.exe
```

To run it, place a compatible `MacII.ROM` beside the executable, then insert or
drag your own disk images into the emulator.

## Private Embedded Builds

The public build disables embedded ROM/disk resources by default:

```c
#define EnableEmbeddedResources 0
```

Do not publish builds that contain ROMs, operating system images, commercial game
disk images, saves, manuals, codes, or game-derived artwork unless you have the
rights to distribute them.

## License

Mini vMac is distributed under GNU GPL v2. See [LICENSE](LICENSE) and
[minivmac/COPYING.txt](minivmac/COPYING.txt).

This is an unofficial custom build and is not affiliated with Gryphel, Apple,
Broderbund, Ubisoft, or Jordan Mechner.

Mini vMac upstream: https://www.gryphel.com/c/minivmac/
