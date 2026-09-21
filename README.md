# Balouch AI

Balouch AI is the official AI assistant for Farhan Balouch.

## Knowledge architecture

`sync.js` crawls `https://farhanbalouch.com`, discovers the sitemap when available, follows same-site links, and writes approved website content to `data/knowledge.js`.

The Vercel serverless endpoint in `api/chat.js` retrieves the most relevant synced pages for each question and sends only that context to the selected AI provider. The complete website knowledge is therefore stored separately from the system instructions instead of being copied into one huge prompt.

## Environment variables

Set the provider keys in Vercel Project Settings → Environment Variables:

- `OPENROUTER_API_KEY`
- `GROQ_API_KEY`
- `GEMINI_API_KEY`

Only the key for the provider you actually use is required.

## Local knowledge sync

```bash
node sync.js
```

This updates `data/knowledge.js`.

## Automatic sync

`.github/workflows/sync-knowledge.yml` runs daily and can also be started manually from GitHub Actions. It commits the updated knowledge file, after which Vercel can redeploy from the GitHub change.
