# PhishGuard — URL Threat Scanner

🌐 **Live Link:** 

A lightweight, client-side URL threat scanner that checks any link against multiple security intelligence sources before you click it. No backend, no data storage — everything runs in the browser.

---

## Features

### Always on — no API key needed

| Feature | Description |
|---|---|
| **URL parser** | Breaks any URL into protocol, hostname, path, query string, and fragment for clear inspection |
| **Heuristic analysis** | Instant pattern-matching across 11 threat indicators |
| **Risk meter** | Visual percentage bar based on how many indicators fired and their severity |
| **Verdict banner** | Combined Safe / Suspicious / High Risk verdict weighing all active checks |

### Heuristic indicators checked

- IP address used as hostname
- `@` symbol trick in URL
- Brand name abuse (PayPal, Amazon, Google, Apple, Microsoft, Netflix, etc.)
- Typosquatting / homoglyph substitution (e.g. `paypa1` → `paypal`)
- Missing HTTPS
- Suspicious subdomain keywords (`login`, `secure`, `verify`, `account`, etc.)
- Suspicious TLDs (`.tk`, `.ml`, `.xyz`, `.ru`, `.zip`, etc.)
- Free hosting platforms (Netlify, GitHub Pages, Vercel, Glitch, etc.)
- Unusually long domain names (40+ characters)
- Sensitive path keywords (`/login`, `/reset`, `/webscr`, `/wp-admin`, etc.)
- Deep subdomain nesting (3+ levels)

### VirusTotal — requires free API key

| Feature | Description |
|---|---|
| **70+ vendor scan** | Checks against 70+ antivirus and threat intelligence engines simultaneously |
| **Detection rate meter** | Shows malicious, suspicious, clean, and undetected vendor counts |
| **Full report link** | Links to the complete VirusTotal report for each URL |

### URLScan.io — requires free API key

| Feature | Description |
|---|---|
| **Live page visit** | Opens the URL in a sandboxed browser and records all activity |
| **Page screenshot** | Real screenshot of what the page looked like at scan time |
| **Threat score (0–100)** | URLScan's own risk score based on page behavior and content |
| **Server intelligence** | Reveals real server IP, hosting country, and web server software |
| **Full report link** | Deep link to URLScan's forensic report |

---

## Getting started

PhishGuard is a single HTML file — no build step, no dependencies to install.

### 1. Download

Save `phishguard.html` anywhere on your computer.

### 2. Open

Open the file directly in any modern browser (Chrome, Firefox, Safari, Edge).

```
open phishguard.html
```

Heuristic analysis works immediately without any configuration.

### 3. Add API keys (optional)

Click **API keys** in the scan box to expand the key panel, then paste your keys.

| Key | Where to get it | Cost |
|---|---|---|
| VirusTotal | [virustotal.com/gui/join-us](https://www.virustotal.com/gui/join-us) | Free |
| URLScan.io | [urlscan.io/user/signup](https://urlscan.io/user/signup) | Free |

Keys are stored only in memory for the duration of your browser session. They are never persisted to disk, localStorage, or any server.

---

## Usage

1. Paste any URL into the input field (with or without `https://`)
2. Press **Scan** or hit Enter
3. Results appear in real time as each check completes

You can also click any of the example pills below the input to test with a pre-loaded URL.

---

## How the verdict works

The final verdict banner combines all active checks:

| Verdict | Conditions |
|---|---|
| **High risk** | VT: 3+ malicious vendors · URLScan: malicious or score ≥ 50 · Heuristics: 2+ high-severity flags |
| **Suspicious** | VT: 1+ malicious or 2+ suspicious · URLScan: score ≥ 20 · Heuristics: 1 high-severity or 3+ total flags |
| **No major threats** | None of the above conditions met |

High-severity heuristic flags (brand abuse, typosquat, IP as hostname, @ symbol) carry more weight than medium-severity ones.

---

## Scan timing

| Check | Typical time |
|---|---|
| Heuristic analysis | Instant |
| VirusTotal (cached) | 1–3 seconds |
| VirusTotal (fresh scan) | ~15–20 seconds |
| URLScan.io | ~16–20 seconds |

VirusTotal and URLScan run in parallel, so the total wait for both live checks is the longer of the two — not the sum.

---

## Privacy & security

- **No data stored.** Nothing is written to disk, localStorage, or any database.
- **No backend.** All logic runs entirely in your browser.
- **API keys stay local.** Keys are held in memory only and cleared when you close the tab.
- **URLs are sent to third-party APIs** (VirusTotal, URLScan.io) when you provide API keys. URLScan scans are submitted as `public` visibility by default — do not scan sensitive or private URLs.

---

## Tech stack

| Layer | Choice |
|---|---|
| Runtime | Vanilla HTML + CSS + JavaScript — zero dependencies |
| Fonts | Roboto Mono (logo / code) · Plus Jakarta Sans (UI) via Google Fonts |
| Icons | Inline SVG |
| Animations | CSS scroll-driven reveal via `IntersectionObserver` |
| APIs | VirusTotal v3 · URLScan.io v1 |

---

## Browser support

Any modern browser released in the last three years. Scroll animations gracefully degrade under `prefers-reduced-motion`.

---
## Limitations

- **Not a replacement for antivirus software.** Heuristics catch patterns, not every threat.
- **New phishing sites can evade detection.** Threat databases take time to update after a new site goes live.
- **Free API tiers are rate-limited.** VirusTotal's free tier allows 4 requests per minute. Scanning many URLs quickly may result in temporary blocks.
- **URLScan public scans are visible to others.** Anyone can search URLScan.io and find your submitted URLs.

---

## License

For personal and security research use only. PhishGuard is not affiliated with VirusTotal or URLScan.io.
