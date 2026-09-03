# OpenStations

A curated, free, and open list of internet radio stations — organized by genre, country, and language. Machine-readable JSON, plus auto-generated M3U and PLS for classic media players.

Use it in your own app, on your NAS, in your car, or wherever you play audio.

## Formats

| File | Purpose |
|------|---------|
| `stations.json` | Master list — all stations with full metadata |
| `by-genre.json` | Stations grouped by genre (Ambient, Jazz, Classical, etc.) |
| `by-country.json` | Stations grouped by ISO 3166-1 country (US, HK, FR, GB, …) |
| `by-language.json` | Stations grouped by BCP 47 language tag (`en`, `zh-HK`, `fr`, …) |
| `stations.m3u` | Standard M3U playlist for VLC, iTunes, foobar2000, and most media players |
| `stations.pls` | PLS playlist for older tools that prefer it |

Auto-generated views regenerate from `stations.json` on every push, so all files stay in sync.

## Quick start

### Grab the raw JSON

```
https://niftyopen.github.io/OpenStations/stations.json
```

### Grab the M3U (drop into VLC or iTunes)

```
https://niftyopen.github.io/OpenStations/stations.m3u
```

### From your app

```swift
let url = URL(string: "https://niftyopen.github.io/OpenStations/stations.json")!
let (data, _) = try await URLSession.shared.data(from: url)
let catalog = try JSONDecoder().decode(RadioCatalog.self, from: data)
```

## Station schema

Each station in `stations.json`:

```json
{
  "id": "somafm-groove-salad",
  "name": "Groove Salad",
  "streamURL": "https://ice1.somafm.com/groovesalad-128-mp3",
  "genre": "Ambient",
  "country": "US",
  "language": "en",
  "bitrate": 128,
  "codec": "mp3",
  "homepage": "https://somafm.com/groovesalad/"
}
```

- `id` — stable identifier, kebab-case
- `country` — ISO 3166-1 alpha-2 code
- `language` — BCP 47 tag
- `codec` — `mp3`, `aac`, `hls`, `ogg`, or `flac`
- `bitrate` — kbps (optional; omit or set null for HLS adaptive
  streams and hosts that don't publish a fixed bitrate)
- `homepage` — station's official page

## License

This project is licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)**.

You are free to use, adapt, and share this list — including commercially. In exchange, please credit OpenStations and link back to this repository.

**Suggested attribution:**

> Radio station list from [OpenStations](https://github.com/niftyopen/OpenStations), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Contributing

Suggestions welcome. See `CONTRIBUTING.md` for how to submit a station or report a broken stream.

## Apps using OpenStations

- **myAddress** for iOS and macOS — Mac monitoring utility with CarPlay radio integration. [App Store](https://apps.apple.com/us/app/myaddress-monitoring-tools/id627535992)

Using OpenStations in your project? Open a PR to add yourself here.

## Support the maintainer

If OpenStations saves you time or helps your project, consider tipping via GitHub Sponsors or Ko-fi (links coming soon).
