# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - Unreleased

### Added
- Interactive wizard: run `video-to-av1` with no arguments (or `convert --interactive`)
- Video resolution option (`--resolution`, never upscales `NNNp` values)
- Constant-quality mode (`--crf` / `-q`) alongside target bitrate
- Folder/file browser: native picker window with automatic terminal fallback (`--no-gui` to force terminal)
- Input validation for bitrate, CRF, preset and resolution

### Fixed
- Progress bar jumped to 100% almost immediately (ffmpeg's `out_time_ms` is microseconds)
- Progress stalled or hung because ffmpeg's stderr pipe was never drained
- Missing-ffprobe case now shows an indeterminate progress bar instead of nothing
- `--dry-run` and "no videos found" no longer print a spurious "Error:" and exit 1
- Real ffmpeg error text is now reported on failure
- `pytest` config used an invalid coverage report type

### Changed
- Command-line flags now take priority over config-file values (previously the reverse)

## [1.0.0] - 2024-01-15

### Added
- Initial release
- Batch video conversion to AV1 format
- Parallel processing support
- Dry-run mode for preview conversions
- Configuration file support (YAML/JSON)
- Cross-platform CLI using Typer
- Auto-detection of FFmpeg from system PATH
- Customizable bitrate and preset options
- Comprehensive logging and error handling
- Extensive documentation and examples
- GitHub Actions CI/CD workflow
- Unit tests with pytest

### Features
- ✅ Single file and folder batch conversion
- ✅ Parallel conversion (multiple files simultaneously)
- ✅ Configurable AV1 encoding parameters
- ✅ Support for 20+ video formats
- ✅ YAML/JSON configuration files
- ✅ Progress tracking and status reporting
- ✅ Windows, macOS, and Linux support
- ✅ Comprehensive command-line help

---

## Future Roadmap

- [ ] Progress bar with ETA
- [ ] Resume interrupted conversions
- [ ] Batch job scheduling
- [ ] Web UI dashboard
- [ ] Integration with cloud storage (S3, Google Drive)
- [ ] Advanced filtering options
- [ ] Hardware acceleration support (NVIDIA, AMD)
- [ ] Subtitle and metadata preservation options
