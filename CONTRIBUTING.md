# Contributing to OpenStations

Thank you for helping keep this list useful. Two common ways to contribute:

## Suggest a new station

Open a PR that edits **only** `stations.json` (auto-generated view files will regenerate on merge).

Add your entry to the `stations` array, following this schema:

```json
{
  "id": "your-station-slug",
  "name": "Station Display Name",
  "streamURL": "https://stream.example.com/high.mp3",
  "genre": "Jazz",
  "country": "US",
  "language": "en",
  "bitrate": 128,
  "codec": "mp3",
  "homepage": "https://example.com/"
}
```

### Field requirements

| Field | Required | Notes |
|-------|----------|-------|
| `id` | ✅ | Unique kebab-case slug (e.g. `wnyc-fm-newyork`) |
| `name` | ✅ | Display name (Title Case) |
| `streamURL` | ✅ | Direct stream URL that plays in any standard player |
| `genre` | ✅ | See genre list below |
| `country` | ✅ | ISO 3166-1 alpha-2 (US, GB, HK, FR, JP, DE, …) |
| `language` | ✅ | BCP 47 tag (`en`, `zh-HK`, `fr`, `ja`, …) |
| `bitrate` | ✅ | kbps as a number |
| `codec` | ✅ | `mp3`, `aac`, `hls`, `ogg`, or `flac` |
| `homepage` | ✅ | Official station page |

### HLS (m3u8) streams

When `codec = "hls"`, `streamURL` MUST point to an `.m3u8` playlist
manifest (e.g. `https://example.com/live/hls/master.m3u8`). AVPlayer
and most modern browsers handle HLS natively.

Notes for contributors:
- Verify the URL returns `Content-Type: application/vnd.apple.mpegurl`
  OR ends in `.m3u8`
- For adaptive HLS with multiple bitrates, record the **highest**
  rendition's bitrate in the `bitrate` field
- HLS uses segmented chunks — less resilient to weak network than
  raw MP3 streams; note stability in the PR if known

**NOT accepted:** playlist indirection files (`.pls`, plain `.m3u`
files that list HTTP URLs). These aren't streams — they're pointers.
Follow the pointer to the actual stream URL and submit that.

### Accepted genres

Use one of: `Ambient`, `Alternative`, `Classical`, `Country`, `Eclectic`, `Electronic`, `Folk`, `Hip-Hop`, `Jazz`, `Latin`, `News / Talk`, `Pop`, `Reggae`, `Rock`, `Soul`, `World`.

If a station really doesn't fit any of these, mention it in the PR — we can extend the list.

### Before you submit

- [ ] The stream URL plays for at least 60 seconds in VLC or a browser tab
- [ ] The station is legally free to listen to (public radio, publicly announced free stream, etc.)
- [ ] The stream is not part of a paid or gated service
- [ ] The `id` slug is unique (search `stations.json` for duplicates)
- [ ] Country, language, and genre fields are filled correctly

Once merged, all view files (`by-genre.json`, `by-country.json`, `by-language.json`, `stations.m3u`, `stations.pls`) will auto-regenerate.

## Report a broken stream

If a station's URL stops working, open an issue using the **"Broken stream"** template. Include:

- Station id
- When you first noticed
- Any error message from your player

A weekly automated health-check also opens issues for streams that fail to respond — you don't have to hunt them down yourself, but reports still help.

## Report a wrong metadata

For fixes like a genre change, wrong country, or renamed station:

- Open a PR editing `stations.json`, OR
- Open an issue with the change if you can't PR

## What we won't accept

- Streams that require login, subscription, or paywall
- Streams that inject ads via the app (short station-ID stingers are fine)
- Streams with unclear or restricted redistribution rights
- Streams hosted on your own infrastructure that you can't guarantee will stay up long-term (occasional exceptions if you're the station operator)

## Questions

Open an issue with the label `question` and we'll get back to you.
