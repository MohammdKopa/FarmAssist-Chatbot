# FarmAssist Chatbot 🌾

Free satellite-powered farming assistant for farmers in Syria and Nigeria.

## What It Does

- Monitors farm health using Sentinel-2 satellite data
- Calculates NDVI (vegetation health index)
- Provides farming tips in Arabic and English
- No cost for farmers

## Files

```
├── index.html              # Web chatbot interface
├── n8n-workflow.json       # Full n8n workflow (Earth Engine)
├── n8n-workflow-simple.json # Simple n8n workflow (Sentinel Hub)
└── README.md               # This file
```

## Quick Start

### Option 1: Demo Mode (No Backend)

1. Just open `index.html` in a browser
2. The chatbot works with simulated data
3. Good for testing the UI

### Option 2: Full Setup with n8n

#### Step 1: Get Satellite Data API Access

**Sentinel Hub (Recommended - Easier)**
1. Sign up at https://www.sentinel-hub.com/
2. Create a new OAuth client
3. Free tier: 30,000 requests/month

**OR Google Earth Engine (Free but complex)**
1. Apply at https://earthengine.google.com/signup/
2. Approval takes 1-3 days
3. Completely free, unlimited usage

#### Step 2: Set Up n8n Workflow

1. Import `n8n-workflow-simple.json` into n8n
2. Configure credentials:
   - Sentinel Hub OAuth2 (or Earth Engine)
   - Anthropic API key (for Claude)
3. Activate the workflow
4. Copy the webhook URL

#### Step 3: Connect Frontend

1. Open `index.html`
2. Find this line:
   ```javascript
   webhookUrl: 'YOUR_N8N_WEBHOOK_URL',
   ```
3. Replace with your n8n webhook URL
4. Host on your VPS or any static hosting

## Hosting Options

### Your VPS (Recommended)
```bash
# Upload to your aaPanel server
scp index.html user@your-vps:/www/wwwroot/farmassist/
```

### Free Options
- GitHub Pages
- Netlify
- Vercel
- Cloudflare Pages

## API Costs

| Service | Free Tier | Notes |
|---------|-----------|-------|
| Sentinel Hub | 30K req/month | ~1000 farms daily |
| Earth Engine | Unlimited | Needs approval |
| Claude API | Pay per use | ~$0.003 per chat |
| n8n | Self-hosted free | Your VPS |

## Customization

### Add More Languages

Edit the `TRANSLATIONS` object in `index.html`:

```javascript
const TRANSLATIONS = {
    en: { ... },
    ar: { ... },
    // Add Hausa for Nigeria:
    ha: {
        welcome: "Sannu! Ni ne mataimakinka na noma 🌾",
        // ...
    }
};
```

### Change Satellite Indices

In the n8n workflow, modify the evalscript to calculate different indices:

- **NDVI**: Vegetation health
- **NDWI**: Water content
- **NDMI**: Moisture stress
- **EVI**: Enhanced vegetation

## Workflow Diagram

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Farmer    │────▶│   Web Chat   │────▶│      n8n        │
│   Browser   │◀────│   (HTML)     │◀────│    Webhook      │
└─────────────┘     └──────────────┘     └────────┬────────┘
                                                  │
                                    ┌─────────────┴─────────────┐
                                    ▼                           ▼
                           ┌──────────────┐           ┌─────────────────┐
                           │ Sentinel Hub │           │   Claude API    │
                           │    (NDVI)    │           │  (Chat/Tips)    │
                           └──────────────┘           └─────────────────┘
```

## Future Ideas

- [ ] WhatsApp bot integration (Twilio)
- [ ] SMS alerts for poor crop health
- [ ] Historical data tracking
- [ ] Weather integration
- [ ] Crop disease detection (ML model)
- [ ] Multi-farm support per user

## Support

This is a free tool for farmers. No commercial use.

---

Made with ❤️ for farmers in Syria and Nigeria
# FarmAssist-Chatbot
