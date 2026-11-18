# Deploy Murojaat EDU (GitHub + Render)

1. Run locally first (README). Rotate any exposed Gemini keys in Google AI Studio. Copy your new key only into the local .env or hosting environment, never into GitHub.
2. Create a GitHub repository named `murojaat-edu`. Upload the contents of the project directory (package.json must be at repo root), including hidden .gitignore and .env.example. Do NOT upload .env, keys, private data or node_modules. Use GitHub Desktop or Git CLI if preferred.
3. At https://dashboard.render.com create a Web Service, connect repo, select Node and Free (if available), build `npm ci`, start `npm start`, health check `/healthz`.
4. Add environment variables: NODE_ENV=production, GEMINI_API_KEY=<fresh key>, GEMINI_MODEL=<working text model>, GEMINI_TTS_MODEL=gemini-3.8-flash-tts, DEMO_ACCESS_CODE=<strong shared password>, ADMIN_ACCESS_CODE=<different strong password>, AI_DAILY_LIMIT=50. Do not set PORT on Render (the platform provides it).
5. Deploy, visit the generated HTTPS URL. Citizen uses `/`, staff uses `/admin`. Give judges the shared demo access code; give only staff the admin code. Test microphone permissions, chat and speech. Free hosting may sleep/restart, deleting demo data. API usage is separately metered; free quotas/model availability are not guaranteed.
6. Use only fictional records. This demo is not a government service. Do not submit actual citizen information, or claim OneID or HEMIS is connected.

## Updating local installation
Extract into a separate folder. Stop the old server (Ctrl+C), open the new folder in VS Code, copy your private settings into the new `.env`, set ADMIN_ACCESS_CODE and GEMINI_TTS_MODEL, then `npm.cmd ci` and `npm.cmd start`. Refresh with Ctrl+F5. If 3000 is occupied stop the other server or use PORT=3001. Do not expose .env in screenshots.
