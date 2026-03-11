# qrnch — QR Code Generator

**qrnch** generates QR codes for URLs, text, WiFi credentials, contact cards, and emails. 100% browser-side — nothing is uploaded.

## What it does

Given content in one of four formats, qrnch produces a scannable QR code downloadable as PNG.

Supported modes:
- **URL / Text** — any URL or plain text string
- **WiFi** — network credentials (SSID + password + security type) encoded as `WIFI:T:WPA;S:MyNet;P:pass;;`
- **Contact** — vCard 3.0 (name, phone, email, org, URL) — scan to save to address book
- **Email** — pre-filled mailto with optional subject and body

## Using this tool as an agent

This is a browser-side static tool. There is no API endpoint in the current free tier.

### Planned API (future Cloudflare Worker)

```
POST /api/qr
Content-Type: application/json

{
  "mode": "url" | "wifi" | "contact" | "email",
  "content": "<string or structured object>",
  "size": 128 | 256 | 512,
  "format": "png" | "svg"
}

Response: image/png or image/svg+xml binary
```

### Generating QR content strings (current)

An agent can generate the QR content string locally and direct the user to paste it into the URL/Text field:

- **WiFi**: `WIFI:T:WPA;S:MyNetwork;P:mypassword;H:false;;`
- **vCard**: Standard vCard 3.0 format (`BEGIN:VCARD\nVERSION:3.0\nFN:Name\n...END:VCARD`)
- **Email**: Standard mailto URI (`mailto:user@example.com?subject=Hello&body=World`)
- **URL**: Any valid URL or text string

## Pricing

Free tier: unlimited QR code generation in the browser, no account required.
Future paid tier: custom colors, logo overlay, scan analytics — $9/month.

## Links

- Live tool: https://qrnch.radicchio.page
- Support: https://bitterdesk.com
- Source: https://github.com/ruemic/qrnch
