# UniGO 🎓

> AI-powered professor discovery platform for IITs & NITs

UniGO helps students find the perfect research mentor by semantically matching their interests to professors across India's top technical institutions — using Claude AI, not just keyword search.

![UniGO Banner](https://img.shields.io/badge/Professors-1583-1a1aff?style=for-the-badge) ![IITs](https://img.shields.io/badge/IITs-16-ff4d00?style=for-the-badge) ![AI](https://img.shields.io/badge/Powered%20by-Claude%20AI-7c3aed?style=for-the-badge)

---

## ✨ Features

- **AI Semantic Matching** — Describe your research passion in plain English. Claude reads your interests and scores every professor on true semantic relevance, not just keyword overlap.
- **Live Profile Scraping** — Fetch any professor's IIT faculty page or Google Scholar profile in real time to get their latest publications and updated research areas.
- **1,583 Real Professors** — Data from 16 IITs across 55+ departments, with verified emails.
- **Smart Chip Filters** — AI automatically highlights the most relevant research area chips based on your description.
- **College Browser** — Explore all IITs with professor counts, departments, and founding year. Click any college to instantly filter professors.
- **Zero cost** — Completely free for students, forever.

---

## 🚀 Live Demo

👉 **[unigo.github.io/UniGO](https://yourusername.github.io/UniGO)**

---

## 🛠️ How It Works

```
Student types interest description
        ↓
Claude AI scores all professors semantically (0–100)
        ↓
Keyword chip filters applied as secondary filter
        ↓
Results ranked by combined AI + keyword score
        ↓
Click professor → modal with email + "Fetch Live Profile"
        ↓
Claude web-searches IIT page + Google Scholar → merges live data
```

### Matching Score Formula
```
Final Score = (AI Score × 65%) + (Keyword Score × 35%)
```
If AI matching hasn't been run, pure keyword scoring is used.

---

## 📁 Project Structure

```
UniGO/
├── index.html          # Redirect to main app
├── UniGO_AI.html       # Main application (self-contained)
└── README.md           # This file
```

The entire app is a **single self-contained HTML file** — no build step, no dependencies, no backend required for basic use.

---

## ⚙️ API Key Setup (for AI features)

The AI matching and live scraping features call the Anthropic API. For production use, you need a backend proxy so your API key isn't exposed client-side.

### Quick local proxy (Node.js)

```bash
npm install express http-proxy-middleware cors
```

```js
// proxy.js
const express = require('express');
const { createProxyMiddleware } = require('http-proxy-middleware');
const cors = require('cors');

const app = express();
app.use(cors());
app.use('/api', createProxyMiddleware({
  target: 'https://api.anthropic.com',
  changeOrigin: true,
  pathRewrite: { '^/api': '' },
  on: {
    proxyReq: (req) => {
      req.setHeader('x-api-key', process.env.ANTHROPIC_API_KEY);
      req.setHeader('anthropic-version', '2023-06-01');
    }
  }
}));

app.listen(3001, () => console.log('Proxy running on :3001'));
```

```bash
ANTHROPIC_API_KEY=your_key node proxy.js
```

Then update the fetch URL in `UniGO_AI.html` from `https://api.anthropic.com` to `http://localhost:3001/api`.

---

## 🗺️ Roadmap

- [ ] NIT dataset integration
- [ ] Professor name search
- [ ] Bookmark / save favourite professors
- [ ] Email template generator ("draft a cold email to this professor")
- [ ] Publication count & h-index display
- [ ] Mobile app (React Native)

---

## 🤝 Contributing

Pull requests welcome! If you have NIT data, professor corrections, or feature ideas — open an issue or PR.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

*Built with ❤️ for Indian students navigating the research landscape.*
