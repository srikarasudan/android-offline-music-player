# Musix – Android Offline Music Player

**Musix** is a simple offline music player for Android, written in **Java**. It plays audio bundled with the app,
so it works without internet access or storage permissions.

![Java](https://img.shields.io/badge/Java-Android-green)
![minSdk](https://img.shields.io/badge/minSdk-21-blue)

## Features

- **Playlist:** tap any song in the list to play it
- **Playback controls:** play/pause, next and previous
- **Shuffle:** when on, *Next* and auto-advance pick a random song
- **Repeat:** when on, the current song plays again when it finishes
- **Seek bar** with elapsed and total time, updated as the song plays
- **Auto-advance** to the next song at the end of a track

Shuffle and repeat are toggles: the icon is dimmed when the mode is off and bright when it's on.

## Tech stack

Java · Android SDK · `MediaPlayer` API · XML layouts · Gradle

| | |
|---|---|
| Min SDK | 21 (Android 5.0) |
| Compile / target SDK | 32 |
| Android Gradle Plugin | 7.2.1 |
| Gradle | 7.3.3 |

## How it works

All playback logic is in [`MusicPlayerActivity.java`](app/src/main/java/com/example/musicappf/MusicPlayerActivity.java):

- Songs are bundled in `app/src/main/res/raw/` and loaded with `MediaPlayer.create(...)`.
- A single `OnCompletionListener` decides what happens at the end of a track: replay it (repeat),
  play a random song (shuffle), or play the next one.
- A `Handler` updates the seek bar and the time labels every 100 ms while music is playing.

## Using your own music

The repository ships with **six short placeholder tones** so it builds and runs out of the box.
To play your own songs:

1. Replace `song1.mp3` … `song6.mp3` in `app/src/main/res/raw/` with your files, keeping the same names.
2. Update the titles and artists in `initializeSongs()` in `MusicPlayerActivity.java`.

Only use music you have the rights to, and don't commit copyrighted songs to a public repository.

## Run it

1. Open the project in **Android Studio**.
2. Let Gradle sync (install SDK 32 if Android Studio asks).
3. Run it on an emulator or a phone with Android 5.0 or later.

## Requirements document and roadmap

[`docs/Musix_SRS.pdf`](docs/Musix_SRS.pdf) is the Software Requirements Specification written for this project.
It describes the full planned app. This repository implements the core player. Still to build from the SRS:

- [ ] Scan the device for audio files instead of bundling them
- [ ] Create and manage your own playlists
- [ ] Notification and lock-screen controls
- [ ] Background playback service

## Project structure

```
app/src/main/
├── java/com/example/musicappf/MusicPlayerActivity.java   # player logic
├── res/layout/activity_music_player.xml                  # UI layout
├── res/drawable/                                         # icons, buttons, album covers
└── res/raw/                                              # audio files (placeholders)
```

**Author:** Srikarasudan P R · [LinkedIn](https://www.linkedin.com/in/srikarasudan-p-r-4b4423212/)
