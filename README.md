# gl-be6300-doom

Run **DOOM** on the GL.iNet **GL-BE6300** router with framebuffer support.

This project is based on [fbDOOM](https://github.com/andreacampanella/fbdoom) and customized to run directly on the framebuffer `/dev/fb0` of the GL-BE6300 (OpenWrt, IPQ5332 SoC).

---

## 🛠 Build Instructions

### 1. Build the Docker Image

```bash
docker build -t aarch64-musl-builder .
```
2. Run the Docker Container
```
docker run --rm -it -v "$PWD":/build aarch64-musl-builder
```
3. Compile fbDOOM for AArch64 MUSL
```
make CC=aarch64-linux-musl-gcc
```
Run on Target (GL-BE6300)

Copy the compiled doom binary and a valid .WAD file (e.g. DOOM.WAD) to the device.

SSH into the router and run:

```
./doom -file /root/DOOM.WAD
```

Display Notes

Output is rendered directly to /dev/fb0

The screen is 76×284 (RGB565)

I_FinishUpdate() includes scaling and rotation logic for correct orientation and aspect ratio

Requirements

A valid DOOM .WAD file (shareware or full)

Write access to /dev/fb0

Ensure gl_screen service is stopped before running:

/etc/init.d/gl_screen stop

To clear screen before launch:

count=$((76 * 284))
for i in $(seq 1 $count); do printf '\x00\x00'; done > /dev/fb0

