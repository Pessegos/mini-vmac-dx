# Mini vMac DX

An unofficial quality-of-life fork of Mini vMac for modern Windows.

This repository contains source code only. It does not include Macintosh ROMs,
Mac OS disk images, games, save disks, or prebuilt executables with embedded
software.

## What This Changes

- Direct3D 9Ex renderer for smoother fullscreen presentation on modern Windows.
- Direct3D 9 fallback, with the original GDI path still available as a last resort.
- Crisp point/nearest scaling for pixel art.
- Arbitrary window and monitor fit scaling without relying on Mini vMac's old
  fixed magnify/32-pixel sizing behavior.
- Full-monitor fullscreen toggled with Alt+Enter.
- View menu and right-click fullscreen controls.
- Resizable window with aspect-aware fit rendering.
- Window maximize behaves like a normal Windows app.
- Alt+Tab and Windows hotkeys are friendlier in fullscreen.
- Windowed mouse behavior uses click-to-capture so resizing and menus stay usable.
- New emulator windows are brought forward and offset when another instance is
  already open.
- Embedded-disk builds can run multiple instances safely: the first instance
  uses the persistent disk, while additional instances receive private temporary
  copies that Windows deletes on exit.
- DPI-aware Windows manifest.

## What Is Not Included

This repo intentionally does not include:

- Apple Macintosh ROM files.
- Mac OS/System disk images.
- Commercial game data.
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
minivmac-dx.exe
```

To run it, place a compatible `MacII.ROM` beside the executable, then insert or
drag your own disk images into the emulator.

## Optional Audio Compatibility

The default build keeps Mini vMac's normal audio behavior. Two opt-in switches
provide compatibility improvements for software using the MIDI Synth 3.45
driver:

```sh
make MDRV_HIFI=1 ASC_STARTUP_MUTE=1
```

- `MDRV_HIFI=1` enables 16-bit reconstruction for the MIDI Synth 3.45 driver
  when its exact code signature is detected. It also repairs the driver's
  370-sample block boundary discontinuity. Other ASC audio falls back to the
  standard sample path.
- `ASC_STARTUP_MUTE=1` suppresses only the short ASC wavetable initialization
  sound at startup.

These are specialized compatibility options and are disabled by default. The
audio correction performs no WAV capture, tracing, denoising, or other
post-processing.

## Private Embedded Builds

The public build disables embedded ROM/disk resources by default:

```c
#define EnableEmbeddedResources 0
```

When embedded resources are enabled in a private build, simultaneous processes
never write to the same extracted disk. Changes made in a secondary instance
are intentionally temporary.

Do not publish builds that contain ROMs, operating system images, commercial game
disk images, saves, manuals, codes, or game-derived artwork unless you have the
rights to distribute them.

## License

Mini vMac is distributed under GNU GPL v2. See [LICENSE](LICENSE) and
[minivmac/COPYING.txt](minivmac/COPYING.txt).

Mini vMac DX is an independent, unofficial fork.

Mini vMac upstream: https://www.gryphel.com/c/minivmac/
