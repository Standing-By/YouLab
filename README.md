# YouLab

**A browser-based audio cue controller for theatre, built around YouTube and local audio files.**

YouLab lets you paste YouTube links (or upload mp3/wav files), arrange them into a cue list, and run them like a proper show control system. Fades, loops, auto-follows, simultaneous playback, hit buttons are all availalbe from a single web page that runs on any device with a browser.

It was built for the drama classroom, but it works anywhere you need quick, reliable sound cue playback. This will NOT replace a proper cue playback software for a public theatre presentation (there are too many failpoints: requires internet, YouTube needs to be working etc.), but is a great replacement for "just running audio" off YouTube or Spotify in class.

## If you already know QLab, GoButton, or SFX6

Think of YouLab as a lightweight version of GoButton or a VERY lightweight version of QLab that uses YouTube URLs instead of local audio files (though it can do those too).

Everything you'd expect is there: fade in, fade out, auto-follow, pre-wait, post-wait (including negative values for overlapping cues), loop modes (infinite or fixed count), duck others, stop others with optional fade time, and Go Actions (Exit Loop, Fade Out/Stop, Fade Out/Go Next).

**Presets** work like GoButton's cue templates. Select a cue and click one of the preset buttons to configure common behaviors in one click:

- **Auto Stop** - plays once, waits for GO
- **Auto-Follow** - starts the next cue when this one ends
- **Start Next Immediately** - fires the next cue at the same time (one GO triggers both)
- **Loop Until GO** - loops infinitely, then fades out and starts the next cue on the next GO press
- **Crossfade Next** - fades out while auto-following, creating a crossfade between cues

**Key differences from QLab/GoButton:**

- YouTube links instead of (or alongside) local files. Paste a URL, the video loads in a small monitor panel, and YouLab controls playback through the YouTube API.
- No MIDI, no OSC, no video output routing. This is audio-only, kept simple on purpose.
- Runs in a browser. No macOS required. Works on Chromebooks, iPads, Windows, Linux, anything with a browser.
- Save files (.youlab) are self-contained JSON. Audio files are embedded as base64, so a single .youlab file contains your entire show.

**Keyboard shortcuts (same philosophy as QLab):**

| Key | Action |
|-----|--------|
| Space | GO |
| Escape | Stop All |
| F | Fade All (5s fade to silence) |
| P | Pause / Resume |
| R | Reset (re-arm cue 1) |
| Up/Down | Navigate cue list |
| Cmd+C | Copy selected cue |
| Cmd+V | Paste cue |
| Delete | Delete selected cue |



## If you've never used show control software

### What is this?

YouLab is a tool for playing sound effects and music during a live performance (a play, a dance show, a presentation, a church service, anything). Instead of fumbling with Spotify playlists or YouTube tabs, you set everything up in advance and then press one big green button each time you need the next sound.

### Why not just use YouTube?

Because in a live show, you need:

- Sounds to start at exactly the right moment, without an interuption from an ad
- Multiple sounds playing at the same time (background music under a sound effect, for example)
- Sounds to fade in and out smoothly instead of just starting and stopping abruptly
- The next track to start automatically when the current one ends
- A way to loop a track until you decide to move on


### How to use it

**Setting up your show:**

1. Open YouLab in Chrome (or any modern browser).
2. Click **+ ADD CUE** to create your first cue.
3. In the inspector panel on the right, paste a YouTube URL into the YouTube field. Or switch to "Audio File" and upload an mp3/wav.
4. Give the cue a name (something you'll recognize during the show, like "Pre-show music" or "Thunder SFX").
5. Adjust settings: set the volume, trim the start/end times if you only want part of the track, add a fade in or fade out, modify the speed.
6. Repeat for every sound in your show.

**Running your show:**

1. Switch to **SHOW** mode using the toggle at the top of the cue list.
2. The first cue will be highlighted green. That's the "armed" cue, the one that will play when you press GO.
3. Press the **GO** button (or hit the spacebar).
4. The cue starts playing (highlighted purple). The next cue turns green, ready for the next GO.
5. Keep pressing GO to advance through your show.
6. If you need to go back, just click any cue in the list to re-arm it, then press GO.

**Color guide:**

- **Green border** = armed, this cue plays next when you press GO
- **Amber border** = on deck, this cue is up after the armed one
- **Purple border** = currently playing

**Saving and loading:**

Click **SAVE** to download your show as a .youlab file. This file contains all your settings and any uploaded audio. Click **LOAD** to open a saved show. Click **NEW** to start fresh.

### Cue list management

- **Drag and drop** cues to reorder them
- **COPY / PASTE** to duplicate cues (or use Cmd+C / Cmd+V)
- **DELETE** to remove the selected cue

### Hit buttons

Hit buttons are for sounds that don't belong in the sequential cue list. Think of them as quick-access buttons for ad-lib sound effects: a doorbell, a phone ring, a rimshot. Click once to play, click again to stop.

To add a hit button, click **+ ADD** in the hits panel at the bottom. Right-click any hit button to edit it.


## Automation features

### Auto-Follow

Turn this on and the next cue will automatically start when the current cue finishes. Chain several cues together with auto-follow to create a playlist that runs itself.

### Post Wait

When auto-follow is on, post wait controls when the next cue starts relative to the end of the current cue:

- **0** = next cue starts the instant this one ends
- **Positive number** (e.g., 3) = waits 3 seconds after this cue ends, then starts the next
- **Negative number** (e.g., -5) = starts the next cue 5 seconds before this one ends, creating an overlap

### Pre-Wait

Delays the start of a cue after GO is pressed. If you set pre-wait to 3 seconds, pressing GO will wait 3 seconds before the cue actually begins playing.

### Go Actions

Go Actions let a single cue respond to GO more than once. Set a Go Action, and the first GO starts the cue. The next GO triggers the action:

- **Exit Loop** - stops looping and lets the cue play to its end
- **Fade Out / Stop** - fades out and stops the cue
- **Fade Out / Go Next** - fades out the cue and starts the next one

### Duck Others

When a cue with "Duck Others" starts playing, all other playing cues drop in volume by a percentage you set. When the ducking cue ends, volumes restore, which is useful for voiceover announcements over background music.

### Stop Others

When a cue with "Stop Others" starts, all other playing cues stop. You can set a fade time so they fade out gracefully instead of cutting off.



## Technical details

### Save file format

Shows are saved as .youlab files, which are plain JSON. YouTube-only shows are tiny (a few KB). Shows with uploaded audio files will be larger because the audio is embedded as base64 data. A typical 4-minute mp3 adds about 5MB. Files over 20MB trigger a warning when uploading.

### Browser compatibility

YouLab works in Chrome, Edge, Safari, and Firefox. Chrome is recommended for the most reliable YouTube playback. Works on Chromebooks, iPads, and phones, though the interface is designed for screens 1024px or wider.
