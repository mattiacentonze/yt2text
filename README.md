# yt2text

A lightweight and fast Bash script to extract transcripts and subtitles from YouTube videos as **clean plain text** or **WebVTT with timestamps**.

Features automatic downloading of manual and auto-generated subtitles, intelligent deduplication of repeated lines (common with scrolling YouTube auto-captions), automatic caching of the standalone `yt-dlp` executable, and pipeable stdout support (`-o -`).

## Prerequisites

The script requires standard Unix utilities available on virtually any modern Linux distribution:
- **Bash** (4+)
- **curl**
- **Python 3** (used internally for clean VTT parsing and text normalization)

No third-party Python packages are required. A standalone, up-to-date `yt-dlp` binary is downloaded automatically on first run and cached in `~/.cache/yt2text/`.

## Installation

```bash
git clone https://github.com/mattiacentonze/yt2text.git
cd yt2text
chmod +x yt2text
ln -s "$(pwd)/yt2text" ~/.local/bin/yt2text
# Optional: create a short alias yt2txt
ln -s "$(pwd)/yt2text" ~/.local/bin/yt2txt
```

## Usage

```bash
# Extract transcript as clean text (defaults to Italian with automatic English fallback)
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o transcript.txt

# Print transcript directly to standard output (pipeable)
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o -

# Preserve timestamps in original WebVTT format
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o subtitles.vtt -t

# Specify a preferred language (e.g. Spanish 'es', French 'fr', English 'en')
yt2text -u "https://www.youtube.com/watch?v=VIDEO_ID" -o text.txt -l en

# Force update the cached yt-dlp binary
yt2text -U -u "https://www.youtube.com/watch?v=VIDEO_ID" -o test.txt
```

### Options

| Option | Description |
|---|---|
| `-u URL` | **Required.** Target YouTube video URL |
| `-o FILE` | **Required.** Output file path, or `-` for standard output |
| `-l LANG` | Preferred subtitle language code (default: `it`, fallback: `en`) |
| `-t` | Keep timestamps and export in original WebVTT format |
| `-U` | Force update the local `yt-dlp` binary in the cache directory |
| `-h` | Display usage help |

## License

Released under the [MIT](LICENSE) License.
