# Video to AV1

A fast and efficient CLI tool to convert videos to AV1 format using FFmpeg.

## Features

- **Interactive mode**: just run `video-to-av1` and answer a few questions
- Choose resolution, quality (CRF) or bitrate, audio bitrate and preset
- Folder/file browser: native picker window, with an in-terminal fallback for SSH/headless
- Batch conversion of single files or folders, with live progress bars
- Parallel processing for faster throughput
- Dry-run mode to preview conversions
- YAML/JSON configuration file support
- Cross-platform (Windows, macOS, Linux)

## Installation

### Prerequisites
- Python 3.8+
- FFmpeg with libsvtav1 support

### From Source

```bash
git clone https://github.com/wizzemraw/video-to-av1.git
cd video-to-av1
pip install -e .
```

## Usage

> **Windows note:** the command is `video-to-av1`. A bare `convert` is a built-in
> Windows disk utility, not this tool. `convert` here is a *subcommand*:
> `video-to-av1 convert ...`

### Interactive mode (easiest)

```bash
video-to-av1
```

You'll be guided through: source file/folder, output folder (with a folder
browser), resolution, quality (CRF) or bitrate, audio bitrate and preset, then
shown a summary before anything starts. Use `video-to-av1 --no-gui` to always use
the terminal browser instead of a picker window.

You can also start the wizard with some answers pre-filled:

```bash
video-to-av1 convert ./videos --interactive
```

### Command-line mode (for scripts)

```bash
# Convert a single file
video-to-av1 convert input.mp4 --output ./converted

# 720p, constant quality (CRF 32)
video-to-av1 convert ./videos -o ./converted -r 720p -q 32

# 1080p at a target bitrate
video-to-av1 convert ./videos -r 1080p -b 1500k

# Parallel processing / preview only
video-to-av1 convert ./videos -o ./converted --parallel 4
video-to-av1 convert ./videos --dry-run
```

### Options

- `--output, -o` : Output folder (default: current directory)
- `--resolution, -r` : `1080p`, `720p`, `1280x720`, ... (default: keep original; never upscales `NNNp`)
- `--crf, -q` : Constant quality 0-63, lower = better (use instead of `--bitrate`)
- `--bitrate, -b` : Target video bitrate (default: 400k; use instead of `--crf`)
- `--preset, -p` : Encoding preset 0-12 (default: 6)
- `--audio-bitrate, -ab` : Audio bitrate (default: 96k)
- `--threads, -t` : Threads per encoding (default: 4)
- `--parallel, -j` : Parallel conversions (default: 1)
- `--suffix, -s` : Output filename suffix (default: _converted)
- `--dry-run, -n` : Preview without converting
- `--config, -c` : Load settings from config file
- `--interactive, -i` : Ask for every setting step by step
- `--no-gui` : Never open a folder-picker window
- `--verbose, -v` : Enable verbose logging

`--crf` and `--bitrate` can't be combined: SVT-AV1 uses constant quality *or* a
target bitrate. Command-line flags override config-file values.

## Configuration

Create a `config.yaml` file:

```yaml
crf: 32            # or: bitrate: "1M"
resolution: 720p
preset: 6
audio_bitrate: "128k"
threads: 8
suffix: "_av1"
```

Then use it:

```bash
video-to-av1 convert ./videos --config config.yaml
```

## Development

```bash
pip install -e ".[dev]"
pytest
```

## License

MIT License
