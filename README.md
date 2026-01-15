# PicoHDMI

An HSTX-native HDMI output library for the RP2350 (Raspberry Pi Pico 2).

PicoHDMI leverages the RP2350's dedicated **HSTX (High-Speed Transmit)** peripheral with hardware TMDS encoding. No bit-banging, no overclocking required: just near-zero CPU overhead for video output.

## Overview

`pico_hdmi` provides a high-performance video and audio output pipeline using the RP2350's HSTX hardware. It is designed to be decoupled from specific application logic, focusing strictly on the generation of stable TMDS signals and Data Island injection (e.g., for audio).

## Key Features

- **HSTX Hardware TMDS Encoding**: Uses the native TMDS encoder for zero-CPU video serialization.
- **Audio Data Islands**: Built-in support for TERC4 encoding and scheduled injection of audio samples.
- **Data Island Queue**: Lock-free queue for asynchronous packet posting from other cores.
- **Double-Buffered DMA**: Stable video output with minimal jitter.

## Directory Structure

- `include/pico_hdmi/`: Public headers. Use `#include <pico_hdmi/...>` in your project.
- `src/`: Implementation files.
- `CMakeLists.txt`: Build configuration.

## Usage

1. Add this directory to your project's `lib` folder.
2. Add `add_subdirectory(path/to/pico_hdmi)` to your `CMakeLists.txt`.
3. Link against `pico_hdmi`.
4. Initialize with `video_output_init()` and run the output loop on Core 1 with `video_output_core1_run()`.

## Development

This project uses `clang-format` and `clang-tidy` to maintain code quality.

### Prerequisites

- **pre-commit**: To automatically run checks before each commit.

On macOS, you can install it via Homebrew:

```bash
brew install pre-commit
```

On Linux:

```bash
pip install pre-commit
```

### Setup Hooks

To activate the git pre-commit hooks, run:

```bash
pre-commit install
```

Once installed, the hooks will automatically format your code and run static analysis whenever you commit.

> **Note**: If a hook fails and modifies your files (e.g., `clang-format`), you will need to `git add` those changes and commit again.

To manually run the checks on all files:

```bash
pre-commit run --all-files
```

## Roadmap for Reusability

For details on the planned transition to a fully generic library, see [REUSABILITY.md](./REUSABILITY.md).

## License

Unlicense
