---
alias: tools
accepts-parameters: false
usage: /tools
name: Tools
author: Blue-EyesWhiteDragon
description: >
        A list of tools that the agent has at their disposal.
version: 1.0.0
topic: Google Flow Music — Instruction
date-format: YYYY-MM-DD
last-updated: 2026-05-08
---

# Flow: Tools

---

## Instructions

List the tools you have at your disposal.

Examples of known tools so far:

## Audio & Editing
- `audio__plan_edit`: Plan complex modifications (extend, replace, effects).
- `audio__render_edit`: Execute planned edits.
- `audio__apply_effect`: Apply discrete effects (Compressor, EQ, Reverb, etc.).
- `audio__split_stems`: Separate a track into Vocals, Drums, Bass, and Other.
- `audio__caption`: Analyze and describe audio content.
- `audio__transcribe`: Extract lyrics from audio.
- `audio__convert_format`: Change file types (WAV, MP3, FLAC, etc.).

## Lyrics & Composition
- `lyrics__create`: Write new song lyrics.
- `lyrics__edit`: Modify existing lyrics.
- `lyrics__register`: Import your own lyrics into the system.
- `audio__create_song`: Generate new tracks from prompts/lyrics.

## Management & Discovery
- `songs__list_songs` / `songs__display_songs`: View and manage your tracks.
- `songs__get_metadata` / `songs__update_metadata`: Handle track info and cover art.
- `songs__get_lyrics_timestamps`: Get word-level timing for surgical edits.
- `playlists__create` / `playlists__update` / `playlists__display_playlist`: Organise your work.

## Visuals & Coding
- `video__propose_music_video` / `video__create_music_video`: Create full music videos.
- `video__create_video_clip`: Generate short visual loops.
- `image__create_image`: Generate or edit album art.
- `code__create_space` / `code__edit_space`: Build and refine interactive studio tools.
- `code__create_audio_visualizer`: Write custom GLSL visualizers.

## Player Control
- `player__play_song` / `player__pause_song` / `player__queue_songs`: Control the studio monitors.
- `player__next_song` / `player__previous_song` / `player__set_volume`: Playback navigation.

## System & Users
- `users__get_user_info` / `users__display_profile`: Session and profile data.
- `system__report_feedback`: Technical reporting.
