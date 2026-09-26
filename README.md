Trying to do a alice32 web emu

# All the files we need:
**Base Code & Build Tools**

* **The XRoar Source Tree:** A complete clone of `[https://github.com/stahta01/xroar](https://github.com/stahta01/xroar)`. This provides the 6803 CPU core, keyboard handling, and the WebAssembly build pipeline.
* **Emscripten SDK (emsdk):** The compiler toolchain required to compile the C codebase into WebAssembly (`.wasm`) and generate the JavaScript shell.
* **Standard C Build Environment:** XRoar uses Autotools to configure its build. You will need `autoconf`, `automake`, `pkg-config`, and `make` installed on your development machine.

**Video Emulation Components**

* **`ef9345.c`:** The Thomson EF9345 video display processor logic you already sourced. You will place this inside XRoar's `src/` directory.
* **`ef9345.h`:** The corresponding C header file exposing the initialization, memory read/write, and video rendering functions. If your source repository did not provide this, you will need to manually write a brief header for the functions contained inside `ef9345.c`.

**System ROMs**

* **`alice32.rom`:** The main Matra Alice 32 operating system and BASIC firmware (matching the `c3854ddf` checksum you identified).
* **`charset.rom`:** The EF9345 character generator ROM containing the font and block graphics data (matching the `b2f49eb3` checksum).

**Custom Integration Files (To be created)**

* **`machine-alice32.c`:** A new C file you must write and add to XRoar's `src/` directory. This acts as the virtual motherboard, defining the specific Alice 32 memory map, loading your two ROMs into the correct memory addresses, and routing the 6803 CPU's I/O instructions directly into the `ef9345.c` logic.
* **`Makefile.am` (Modified):** You will need to edit XRoar's existing makefile configuration to ensure your new `machine-alice32.c` and `ef9345.c` files are included during the compilation process.

Do you have a Linux environment, macOS, or Windows Subsystem for Linux (WSL) ready to install the Emscripten SDK and run the Autotools build?

FORK FROM:

MC-10 Javascript Emulator
=========================

Browser based emulation of the Motorola MC6803 CPU and MC6847 VDG. HTML Canvas support is required for rendering. Sound is emulated, but not 100% accurate due to Javascript timing limitations. Cassette loading is supported by simply writing the data directly to memory rather than the traditional cload/m. Graphics modes supported include (SG4/SG6/RG2/CG3).

### Try It!
https://mc-10.com
