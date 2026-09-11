# Decima

A ten-key piano that runs in a browser. No samples, no libraries, no build step — one HTML file and a service worker.

**Play it: https://www.muhassinbabumm.live/piano/**

## Playing

| Input | What it does |
| --- | --- |
| `1` … `0` | The ten white keys, C4 up to E5 |
| `q` `w` `r` `t` `y` `i` `o` | The sharps, sitting on the letters physically above them |
| `space` | Sustain, held down like a pedal |
| Click / tap | Same as the keys; dragging across the board glides |

Striking lower down a key plays a little louder, the way leverage works on a real action.

## Controls

- **Octave** — shifts the whole board, C2 through C6, for tunes that reach past the ten keys.
- **Note names** — swaps the `1`–`0` labels for `C D E F G A B`.
- **Record / Play** — captures what you play with its timing, and replays it. The take survives a reload.
- **Song guide** — lights the next key of a tune and waits for you to find it. Four tunes included.
- **Rotate** — turns the keyboard sideways for playing with the phone held long-ways, useful when the device's rotation lock is on.
- **Sustain** — hold `space` for momentary, or press the button to latch it.

Octave, labels, sustain, and rotation are all remembered for next time.

## How the sound works

Every note is synthesized on the spot with the Web Audio API. Seven sine partials, tuned slightly sharp of the harmonic series because real strings are inharmonic, each decaying at its own rate with the upper ones dying first. A short burst of bandpassed noise gives the hammer its knock, a lowpass sweep opens and closes the tone, and a generated impulse response adds a little room. Low notes ring longer than high ones.

Audio starts on the first key press, since browsers require a gesture before any sound.

## Installing

The site is a PWA. Chrome, Edge, and Android show an "Install as an app" button below the keyboard. On iPhone and iPad, use Share, then Add to Home Screen. Once installed it works with no connection.

## Files

```
index.html               the whole instrument
sw.js                    offline cache
manifest.webmanifest     app metadata
icon-192.png             app icons
icon-512.png
icon-maskable-512.png
apple-touch-icon-180.png
favicon-32.png
og-image.png             link preview
```

## Editing it

Everything lives in `index.html`. The key map is the `WHITE` and `BLACK` arrays near the top of the script; tunes are in `SONGS`, written as sequences of keyboard characters so they transpose with the octave control for free.

**After any change, bump `CACHE` in `sw.js`** — `decima-v4` to `decima-v5` and so on. Without that, anyone who has already loaded the site keeps getting the old files from cache.

## Browser notes

- Needs HTTPS for the service worker; `http://` won't install.
- The silent switch on an iPhone mutes Web Audio entirely, regardless of volume.
