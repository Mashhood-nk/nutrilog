# NutriLog 🥗

A private, AI-powered daily nutrition tracker built for a small group of friends and family tracking their health journey together.

## What it does

- **Log meals** by typing or taking a photo — AI estimates calories, protein, carbs, fat and fibre
- **Smart meal parsing** — type multiple items at once, AI identifies and estimates each separately
- **Running daily totals** — see your nutrition accumulate throughout the day
- **Weight graph** — track weight over time with trend line and 7-day moving average
- **AI Health Coach** — analyses your full history and personal profile, gives personalised advice
- **Daily summary** — log weight, steps and water, generate a one-tap WhatsApp summary for your group
- **Export to Excel** — download all your data anytime
- **Private & invite-only** — access codes per person, admin panel to manage users

## Tech stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML + Vanilla JS, hosted on GitHub Pages |
| Backend | Cloudflare Workers (JavaScript) |
| Database | Cloudflare D1 (SQLite) |
| AI — OpenAI | GPT-5.5 with structured output schema |
| AI — Claude | Claude Sonnet 4.6 with tool use |
| AI — Gemini | Gemini 2.0 Flash |
| Graphs | Plotly.js |
| Excel export | SheetJS |

## Architecture

```
Browser (GitHub Pages)
       ↓
Cloudflare Worker  →  D1 Database
       ↓
OpenAI / Claude / Anthropic APIs
```

## Features

### Meal Logging
Type your meal in any format — comma separated, new lines, or all in one go. The AI intelligently identifies individual items and estimates nutrition for each before summing totals.

### AI Provider Selection
Users can choose their preferred AI provider in Settings:
- **OpenAI GPT-5.5** — highest accuracy (default)
- **Claude Sonnet 4.6** — excellent for South Asian and Arabic food
- **Gemini 2.0 Flash** — fast with free tier available

### Structured Outputs
Both OpenAI (JSON schema) and Claude (tool use) are configured with structured outputs — the AI is forced to return exactly the right fields with no extra text, eliminating parse errors.

### Personal Profiles
Each user sets up their profile once — age, gender, height, target weight, goal, activity level, location and notes. The AI Coach uses this to give genuinely personalised advice.

### Admin Panel
Accessible only with the admin code. Add or remove users without touching any configuration files. Users are stored in D1 — no hardcoded codes anywhere.

## Deployment

### Frontend
Hosted on GitHub Pages. Any push to `main` branch auto-deploys.

### Worker
```bash
cd nutrilog-worker
wrangler deploy
```

### Environment Variables (Cloudflare Secrets)
```bash
wrangler secret put ANTHROPIC_KEY
wrangler secret put OPENAI_KEY
wrangler secret put ADMIN_CODE
```

### D1 Database
Initialise tables by visiting:
```
https://your-worker.workers.dev/init-db
```

## Cost

Approximately **$1.50–4/month** for 5 users logging 3–5 meals/day using GPT-5.5. Claude and Gemini options are significantly cheaper.

## Built by

Mashhood N K — Clinical Research Assistant, Hamad Medical Corporation, Qatar.  
Built to solve a real daily problem: replacing a manual WhatsApp + ChatGPT + Google Sheets workflow with one clean tool.

---

*This is a private app. Access is by invitation only.*
