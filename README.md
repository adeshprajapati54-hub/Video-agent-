# 🎬 Video Agent

Turn any written script into a **narrated video with voiceover** — automatically.

```
script (.txt/.md)  →  scenes  →  voiceover (TTS)  →  visuals  →  video (.mp4 + .srt)
```

## Features

- **Script parsing** — understands `## Heading` scene markers, `[Scene N]` markers, or plain paragraphs
- **Natural voiceover** — powered by `edge-tts` (400+ neural voices), with `gTTS` as automatic fallback
- **Styled visuals** — clean gradient slides rendered per scene (title, narration text, scene badge)
- **Captions** — writes an `.srt` subtitle file alongside the video
- **Zero manual editing** — one command produces a finished, upload-ready MP4

## Requirements

- Python 3.10+
- Packages: `moviepy`, `edge-tts`, `gTTS`, `Pillow`

```bash
pip install moviepy edge-tts gTTS pillow
```

## Quick Start

```bash
# Demo with the included sample script
python3 video_agent.py examples/sample_script.txt -o demo.mp4

# Your own script, Indian English voice
python3 video_agent.py my_script.txt -o my_video.mp4 \
    --title "Product Demo" --voice en-IN-NeerjaNeural

# Faster narration, no captions
python3 video_agent.py my_script.txt --rate "+15%" --no-captions

# See all available voices
python3 video_agent.py --list-voices
```

## Writing a Script

**Option A — scene headings (recommended):**

```text
## Opening Hook
Your first scene's narration goes here.

## Main Point
The next scene continues the story.
```

**Option B — plain paragraphs** (blank-line separated; long paragraphs are auto-chunked):

```text
First paragraph of narration.

Second paragraph of narration.
```

## CLI Options

| Flag | Description | Default |
|---|---|---|
| `script` | Path to the script file | (required) |
| `-o, --output` | Output MP4 path | `output_video.mp4` |
| `-t, --title` | Title shown on slides | `AI Video Agent` |
| `--voice` | edge-tts voice ID | `en-US-JennyNeural` |
| `--engine` | `auto`, `edge`, or `gtts` | `auto` |
| `--rate` | Speech rate, e.g. `+10%` | `+0%` |
| `--pitch` | Speech pitch, e.g. `+2Hz` | `+0Hz` |
| `--no-captions` | Skip the `.srt` file | off |
| `--fps` | Output frame rate | `24` |
| `--list-voices` | List voiceover voices | — |

## Popular Voices

| Voice | Accent |
|---|---|
| `en-US-JennyNeural` | US English (female) |
| `en-US-GuyNeural` | US English (male) |
| `en-IN-NeerjaNeural` | Indian English (female) |
| `en-IN-PrabhatNeural` | Indian English (male) |
| `hi-IN-SwaraNeural` | Hindi (female) |
| `en-GB-SoniaNeural` | British English (female) |

## How It Works

1. **Parse** — the script is split into scenes (headings, markers, or paragraphs)
2. **Speak** — each scene's text is synthesized to audio (edge-tts, falling back to gTTS)
3. **Draw** — each scene gets a styled 1280×720 slide with title + narration
4. **Assemble** — moviepy/ffmpeg chains image + audio clips into one MP4
5. **Caption** — an SRT file with per-scene timings is written next to the video

## Project Files

```
video_agent.py            # the agent (CLI entry point)
examples/sample_script.txt # demo script
README.md                  # this file
```
