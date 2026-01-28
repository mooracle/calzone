# Calzone

Calendar timezone proxy that just works.

Outlook exports calendars with Windows timezone names. Google Calendar expects IANA standard names. Calzone sits in between and translates—fixing the +1 hour offset issue.

---

## How It Works

1. You subscribe to your Outlook calendar via Calzone URL
2. Calzone fetches the calendar from Outlook
3. Converts Windows timezone names (e.g., `Romance Standard Time`) to IANA (e.g., `Europe/Stockholm`)
4. Returns the fixed calendar to Google

No data stored. No accounts required.

---

## Usage

Replace `outlook.office365.com` with `calzone.mooracle.io` in your calendar URL:

```
# Before
https://outlook.office365.com/owa/calendar/.../calendar.ics

# After
https://calzone.mooracle.io/owa/calendar/.../calendar.ics
```

Then add to Google Calendar:
1. Open Google Calendar
2. Click **+** next to "Other calendars"
3. Select **From URL**
4. Paste your calzone URL
5. Click **Add calendar**

---

## Deploy Your Own

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/mooracle/calzone)

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [Cloudflare account](https://dash.cloudflare.com/sign-up) (free tier works)

### Setup

```bash
# Clone the repository
git clone https://github.com/mooracle/calzone.git
cd calzone

# Install dependencies
npm install
```

### Deploy

```bash
# Login to Cloudflare (opens browser)
npx wrangler login

# Deploy to Cloudflare Workers
npm run deploy
```

After deployment, you'll get a URL like:
```
https://calzone.<your-account>.workers.dev
```

### Custom Domain (Optional)

To use your own domain (e.g., `calzone.yourdomain.com`):

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Navigate to **Workers & Pages**
3. Click on **calzone**
4. Go to **Settings** → **Domains & Routes**
5. Click **Add** → **Custom Domain**
6. Enter your subdomain (e.g., `calzone.yourdomain.com`)
7. Click **Add Custom Domain**

Cloudflare handles DNS automatically if your domain is on Cloudflare.

---

## Configuration

Edit `wrangler.toml` to change the target host:

```toml
[vars]
TARGET_HOST = "outlook.office365.com"
```

---

## Timezone Mapping

Uses the official [Unicode CLDR](https://github.com/unicode-org/cldr/blob/main/common/supplemental/windowsZones.xml) mapping—the same authoritative source used by operating systems worldwide. Supports 140+ Windows timezone identifiers.

---

## License

MIT

---

Built by [Mooracle](https://mooracle.io)
