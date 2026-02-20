PocketSNES for TI Nspire CX
==========================

Port done by gameblabla.

PocketSNES was originally a SNES emulator by Nebuleon for GCW0.
Audio (SPU/APU) has been removed since the TI-Nspire does not officially support sound.

It runs well on the TI-Nspire CX thanks to auto-frameskipping and a built-in frame rate
limiter that keeps games running at the correct speed.  Overclocking will improve
performance on demanding games.

Incompatible games:

- Far East of Eden Zero
- Street Fighter Alpha 2
- Star Ocean

These three games use the SDD1 chip; Snes9x 1.43 requires a graphics pack for them.

BUILDING FROM SOURCE
====================

### Prerequisites

You need the **Ndless SDK** which provides the ARM cross-compiler (`nspire-gcc`/`nspire-g++`)
and the packaging tools (`genzehn`, `make-prg`).

**Install on Linux / macOS / Windows (WSL):**

```bash
# 1. Clone the Ndless repository
git clone --recursive https://github.com/ndless-nspire/Ndless.git
cd Ndless

# 2. Build and install the toolchain (~10–20 min)
ndless-sdk/toolchain/build_toolchain.sh

# 3. Add the toolchain to your PATH (add this line to ~/.bashrc or ~/.zshrc too)
export PATH="$PATH:$HOME/ndless/ndless-sdk/toolchain/install/bin"
export PATH="$PATH:$HOME/ndless/ndless-sdk/tools"
```

You will also need standard build tools:

```bash
# Debian / Ubuntu
sudo apt install make zip git build-essential libgmp-dev libmpc-dev libmpfr-dev texinfo

# macOS (Homebrew)
brew install make zip git gmp libmpc mpfr
```

### Build

```bash
# Clone this repository
git clone https://github.com/Maxi2555/pocketsnes-nspire.git
cd pocketsnes-nspire

# Build the .tns file
make -f Makefile.nspire
```

This produces **`pocketsnes.tns`** (and `PocketSNES-nspire.zip` containing the `.tns` and
`README.md`).

To clean build artifacts:

```bash
make -f Makefile.nspire clean
```

### Transfer to the calculator

1. Connect your TI-Nspire CX to your computer via USB.
2. Open **TI-Nspire Student Software** (or **TI Connect CE**) and transfer `pocketsnes.tns`
   to the `/documents/ndless/` folder on the calculator.
3. On the calculator, navigate to the file and press **Enter** to launch it.
   (Ndless must already be installed on the calculator.)
4. Place your ROM files (`.sfc`, `.smc`, or `.zip`) in `/documents/ndless/` as well and pass
   the path as an argument, or use the launcher script bundled with Ndless.

CONTROLS
========

| Calculator key | SNES button |
|----------------|-------------|
| CTRL           | A           |
| SHIFT          | B           |
| VAR            | X           |
| DEL            | Y           |
| TAB            | L           |
| MENU           | R           |
| ENTER          | Start       |
| MINUS (–)      | Select      |
| Arrow keys / 4 5 6 8 | D-pad |
| 7 / 9          | Up-Left / Up-Right diagonal |
| 1 / 3          | Down-Left / Down-Right diagonal |

IN-GAME MENU (press ESC)
========================

Press **ESC** during gameplay to open the in-game menu.

| Menu key       | Action                              |
|----------------|-------------------------------------|
| Up / Down      | Navigate menu items                 |
| Left / Right   | Change selected option value        |
| CTRL (A)       | Confirm selection                   |
| SHIFT (B)      | Resume game                         |
| ESC            | Resume game                         |

Menu options:

- **Resume Game** – return to the game
- **Frameskip: Auto / 1–6** – *Auto* limits the emulator to the correct frame rate
  (60 fps NTSC / 50 fps PAL) and skips rendering when the calc is too slow to keep up.
  Values 1–6 force a fixed number of frames skipped between each rendered frame (useful
  when the device is too slow even in Auto mode).
- **Reset Game** – soft-reset the current ROM
- **Exit** – save SRAM and exit the emulator
