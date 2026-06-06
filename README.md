# AI Chatbot Widget

An embeddable AI chatbot widget built with Cloudflare Workers, Workers AI (Llama 3), Vectorize (RAG), and KV.

## Features
- Real-time streaming AI responses
- FAQ answering via RAG (Retrieval Augmented Generation)
- Persistent conversation history
- Dark/light mode
- Embed on any website with one script tag

## Deploy in GitHub Codespaces (Recommended)

### Step 1 — Open in Codespaces
Click the green **Code** button above → **Codespaces** → **Create codespace on main**

### Step 2 — Login to Cloudflare
```bash
wrangler login
```

### Step 3 — Create KV namespace
```bash
npx wrangler kv namespace create CHAT_SESSIONS
```
Copy the `id` from the output and replace `REPLACE_WITH_YOUR_KV_ID` in `wrangler.jsonc`

### Step 4 — Create Vectorize index
```bash
npx wrangler vectorize create faq-vectors --dimensions=768 --metric=cosine
```

### Step 5 — Deploy
```bash
npm run deploy
```

### Step 6 — Seed the FAQ database
```bash
curl -X POST https://YOUR-WORKER-URL.workers.dev/api/seed
```

## Embed on Any Website
```html
<script>
  window.CHATBOT_BASE_URL = "https://YOUR-WORKER-URL.workers.dev";
  window.CHATBOT_TITLE = "Support";
  window.CHATBOT_GREETING = "👋 How can I help you today?";
</script>
<script src="https://YOUR-WORKER-URL.workers.dev/widget.js"></script>
```

## Cloudflare Free Tier Limits
| Service | Free Limit |
|---|---|
| Workers | 100,000 requests/day |
| Workers AI | 10,000 neurons/day |
| Vectorize | 5M vector operations/month |
| KV | 100,000 reads + 1,000 writes/day |