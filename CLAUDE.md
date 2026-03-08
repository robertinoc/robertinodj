# ROBERTINOC DJ Website

Personal artist page for **ROBERTINOC** — Argentine DJ and producer (Techno · Hard Techno · Bounce · Psy · Acid).

**Live URL:** music.robertino.world

## Tech Stack

- **Plain HTML/CSS/JS** — single-file website (`index.html`), no build tools or frameworks
- **Bilingual (ES/EN)** — JS-based i18n system with `data-i18n` attributes; Spanish default, English secondary
- **Google Fonts** — Rajdhani (headings) + Inter (body)
- **Font Awesome 6** — brand & UI icons (via CDN)
- **YouTube Data API v3** — auto-fetches latest 3 videos from the MUSIC channel (@robertinoc)
- **Spotify Embed** — dark-themed artist iframe (no auth needed)
- **SoundCloud Widget Embeds** — 3 iframe players with real featured tracks
- **EmailJS v4** (`@emailjs/browser`) — contact form submission (no backend needed)
- **CSS custom properties** — "ACID NOIR" dark palette
- **IntersectionObserver** — scroll reveal animations
- **Pure JS Lightbox** — gallery image viewer with Escape key support

## Project Structure

```
robertinodj/
├── index.html                      # Main (and only) code file — all HTML, CSS, JS inline
├── PROFILE.jpg                     # Professional DJ portrait — circular hero avatar
├── ROBERTINOC - PRESSKIT.pdf       # Presskit PDF (~2.2 MB) — local download
├── gallery/                        # Photo gallery images (6 photos)
│   ├── Copy of A86197B2-FE67-4FD8-9CF3-FBEF9DAC4C36.jpeg
│   ├── Copy of IMG_3952(1).jpg
│   ├── Copy of IMG_4137.jpg
│   ├── Copy of IMG_4290.JPG
│   ├── Copy of IMG_4332.jpg
│   └── PROFILE OCT25.jpg
└── CLAUDE.md                       # This file
```

## Development

```bash
python3 -m http.server 8083
```

Or use the Claude Code preview: configured in `robertinotalk/.claude/launch.json` as `dj2`.

## Site Sections

1. **Hero** — Dark gradient background with psychedelic CSS overlay, circular `PROFILE.jpg` avatar above name, white "ROBERTINO" + red "C" text, genre tags, social icon row
2. **SoundCloud** — Title: "Latest Sets on SoundCloud" / "Últimos Sets en SoundCloud". 3 real featured track embeds + "Listen more on SoundCloud" button (SC orange)
3. **YouTube** — Latest 3 videos from MUSIC channel (`@robertinoc`, ID: `UCP7rYFgI41uGFm6tf9Gs-9g`) + "Watch more on YouTube" button (YT red)
4. **Spotify** — Dark-themed artist embed iframe + "Follow me on Spotify" button (Spotify green)
5. **Links (Música)** — Styled cards: latest sets, presskit (local PDF download), "Buy My Music" (Beatport, orange accent), Traxsource
6. **Streaming platforms** — Pill grid with brand-color hovers: Spotify, Apple Music, Amazon, Deezer, TIDAL, SoundCloud, YouTube
7. **About (Sobre mí)** — Bilingual bio + stats (02 EPs, 04 Labels, 03 Collabs Reloaded)
8. **Booking** — 2 side-by-side CTAs: "Send Email" (filled red, opens mailto) + "Contact Form" (outlined, scrolls to #contact)
9. **Gallery** — Responsive CSS grid (3-col desktop, 2-col mobile) with 6 photos + pure JS lightbox
10. **Technical Rider** — 4 cards with red glow hover effect: CDJ+Mixer, Traktor, Controllers, Booking Info
11. **Contact** — Form with 4-layer spam protection + EmailJS
12. **Footer** — All social/platform links + copyright 2026

## Navigation

- **Hamburger menu** — Slide-in sidebar from right, with overlay backdrop
- **Menu items:** SoundCloud, YouTube Music, Spotify Music, Music Links, About Me, Contact
- **Language toggle:** `ES | EN` pill button in the nav bar
- Both hamburger and lang toggle are bilingual (menu items translate)
- Escape key closes both hamburger menu and lightbox

## API Configuration

### YouTube Data API v3 (MUSIC channel)
```js
const YT_API_KEY    = 'AIzaSyA1eLv-LN_loRWLfUQv8XxeUiJyehWLBFo';
const YT_CHANNEL_ID = 'UCP7rYFgI41uGFm6tf9Gs-9g';  // @robertinoc MUSIC channel
```
- **IMPORTANT:** This is the DJ/music channel, NOT the robertinotalk channel (UCTdd_SVBnnVfzJCO05y-MNQ)
- Fetches 3 latest videos via `youtube.googleapis.com/youtube/v3/search`
- Variable-level cache (`cachedYT`) avoids re-fetching on language toggle

### SoundCloud Embeds (real featured tracks)
Three iframe widgets with real track URLs:
1. `special-set-baila-minitel-madrid-211125-psy-hard-techno`
2. `back-2-darkness-original-mix`
3. `robertinoc-enjoy-the-hard-2`

### Spotify Embed
```
https://open.spotify.com/embed/artist/2jkuh1rhF7xhWCjUvBBbGr?theme=0
```

### EmailJS
```js
const EJS_KEY      = 'YOUR_EMAILJS_PUBLIC_KEY';
const EJS_SERVICE  = 'YOUR_EMAILJS_SERVICE_ID';
const EJS_TEMPLATE = 'YOUR_EMAILJS_TEMPLATE_ID';
```
The EmailJS template must include these variables:
- `{{to_email}}` — recipient (robertinoc@gmail.com)
- `{{from_name}}` / `{{from_email}}` / `{{reply_to}}` / `{{subject}}` / `{{message}}`

## Color Palette ("ACID NOIR")

| Variable          | Value                        | Description        |
|-------------------|------------------------------|--------------------|
| `--bg`            | `#0a0a0a`                    | Pitch black        |
| `--bg-card`       | `#111111`                    | Card background    |
| `--primary`       | `#ff1744`                    | Electric red       |
| `--primary-glow`  | `rgba(255,23,68,0.35)`       | Red glow           |
| `--accent`        | `#ff6600`                    | Acid orange        |
| `--text`          | `#ffffff`                    | White              |
| `--text-muted`    | `#888888`                    | Muted grey         |

## Section CTA Buttons (brand colors)

| Button             | Brand Color | CSS Class        |
|--------------------|------------|------------------|
| SoundCloud         | `#FF5500`  | `.cta-soundcloud` |
| YouTube            | `#FF0000`  | `.cta-youtube`    |
| Spotify            | `#1DB954`  | `.cta-spotify`    |

## Contact Form Security (4 layers)

1. **Honeypot** — Hidden `#dj_website` field; bots fill it → silently fake-success
2. **Time-based** — Rejects submissions faster than 3 seconds (bot speed)
3. **Rate limit** — 60s cooldown via `localStorage` key `dj_lastSubmit`
4. **Sanitization** — Trim + length cap all inputs; strip `\r\n\t` from subject line

## Social / Platform Links

| Platform    | URL |
|-------------|-----|
| SoundCloud  | https://soundcloud.com/robertinook |
| YouTube     | https://www.youtube.com/@robertinoc |
| Spotify     | https://open.spotify.com/artist/2jkuh1rhF7xhWCjUvBBbGr |
| Apple Music | https://music.apple.com/co/artist/robertinoc/1237013674 |
| Instagram   | https://instagram.com/robertinoc_music |
| TikTok      | https://tiktok.com/@robertinook |
| Beatport    | https://www.beatport.com/artist/robertinoc/588106 |
| Traxsource  | https://www.traxsource.com/artist/363200/robertinoc |
| Amazon Music| https://music.amazon.com/artists/B071F94BR3/robertinoc |
| Deezer      | https://deezer.com/es/artist/12557510 |
| TIDAL       | https://listen.tidal.com/artist/8776248 |

## Notes

- `PROFILE.jpg` (5.2 MB) — consider compressing for production
- Gallery filenames have spaces — always URL-encode in `src` attributes
- Font Awesome 6 Free is used; Beatport/Traxsource/Deezer/TIDAL use generic FA icons
- `formLoadTime` is set at script init (page load) — do not move it inside the form handler
- YouTube API key is shared with the robertinotalk site but uses a DIFFERENT channel ID
- Hero uses dark gradient background (not PROFILE.jpg as wallpaper) for better text contrast
- Technical Rider cards have red glow hover: `box-shadow: 0 0 25px rgba(255,23,68,0.35)`
