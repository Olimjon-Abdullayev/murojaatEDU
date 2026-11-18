# Murojaat EDU — v0.2
Independent GovTech hackathon prototype, education challenge 1. Not affiliated with OneID, my.gov.uz or any government institution. Only fictional records and public source summaries. Never enter real personal information, credentials or recordings containing sensitive information.

## Windows setup
Node.js 22+ and VS Code. Extract this ZIP into a NEW folder; don't overwrite a working project until tested. In VS Code open the extracted `murojaat-edu` folder. PowerShell:

```powershell
npm.cmd ci
Copy-Item .env.example .env
notepad .env
npm.cmd start
```

Set GEMINI_API_KEY to a fresh Google AI Studio key privately. If upgrading, copy only your private configuration into the new .env. Keep GEMINI_MODEL from your currently working installation if different. Set ADMIN_ACCESS_CODE to a unique password. Local fallback only: `edu-local-2026`. Keep DEMO_ACCESS_CODE blank locally, set a strong shared password for hosted demo. Browse http://localhost:3000 (citizen) or http://localhost:3000/admin (staff). No visible links between portals. Both use separate cookies and backend authorization. Stop with Ctrl+C. Test via `npm.cmd test`.

## Demonstration
1. Citizen home: counts from the shared in-memory case store refresh every five seconds. Feedback is fictional seed data.
2. Sign in: choose **Demo OneID**. The official OneID button only opens the external identity portal; it does not establish a local session. No real credentials are collected. Login help is available. All demo citizens use the same fictional profile; their appeals are isolated by session.
3. My documents: view synthetic GPA, grades, scholarship, diploma metadata and school attestation. No actual official documents are issued.
4. Chat: type a question; choose Uzbek, Russian, Tajik, Karakalpak or English. Gemini receives the requested language and public-source summaries (keyword retrieval), recent conversation, and an authorized synthetic profile. Navigation and major controls are translated; underlying legal summaries, demo data and some notices remain Uzbek/English. Offline answers are Uzbek. Legal answers are informational, not official decisions. No full legal corpus or automated legal compliance certification is included.
5. Ask about a missing scholarship. The AI assistant offers an application action. If not logged in, demo identity is required; after login, the prepared draft appears. Confirm to send to the shared **demo** inbox; a case number is issued. No real submission is made.
6. Staff: open /admin manually and enter ADMIN_ACCESS_CODE. View cases, generate AI response drafts, set in progress, approve response. Trigger 15 synthetic complaints for the radar. The citizen sees status and approved replies in My appeals. Real ministry staff roles/SSO are not included.
7. Voice: allow microphone access in Chrome/Edge on localhost or HTTPS. Voice message records up to 30 seconds and places Gemini transcript in the editable input; press Send. Voice conversation enables turn-based recording, automatic submission, and Gemini TTS playback; click microphone for each new turn. It is not continuous duplex Gemini Live. Use Listen on any assistant message. If TTS fails, browser speech synthesis fallback is attempted (voice/language availability varies). Text API and TTS model IDs are configurable; availability, quotas, and pronunciation vary by account and language. No live provider credentials used in tests. Every transcript, response and speech request counts toward budget. Audio is sent to Gemini only after a deliberate record action; not stored in local database. Avoid personal/sensitive audio. Browser microphone permission is required.

## Architecture
Node.js HTTP server and vanilla JavaScript/CSS, no dependencies. `server.js` implements separate session cookies, role-checked APIs, draft confirmation, data filtering, rate budgets, shared aggregate data, and CSP. `src/ai.js` integrates Gemini text and source IDs. `src/voice.js` integrates audio transcription and TTS; PCM is wrapped in WAV. `src/core.js` contains demo rules, records and radar. `data/knowledge.json` contains public-link summaries rather than a legally verified law database. State is RAM-only; restart clears all cases. Session-scoped case ownership is not a production identity solution. The admin code is demo authentication, not enterprise security. The repository must contain no `.env`, real records, secrets or API keys. Before production: approved identity and government APIs, persistent DB, verified source ingestion, access control and audit, approved data processing/localization and security review, and human authorization for legal decisions.

## APIs
Citizen: /api/session, /api/login, /api/state, /api/chat, /api/transcribe, /api/speak, /api/draft, /api/submit, /api/logout. Staff: /api/admin/session, /api/admin/login, /api/admin/state, /api/admin/chat, /api/admin/update, /api/admin/simulate, /api/admin/logout. POST requests require session CSRF header; no credentials in URL. Only the admin can act on cases. Aggregated public counts contain no personal records.

See DEPLOY.md for free hosting. API docs: https://ai.google.dev/gemini-api/docs/audio and https://ai.google.dev/gemini-api/docs/generate-content/speech-generation.

## Version 3 additions

- Five independent synthetic citizen profiles: student, graduate, pupil, teacher and former teacher. Choose one at demo sign-in; sign out before changing identity.
- 19 downloadable, watermarked demonstration PDFs served only to the signed-in citizen for that profile. These are pre-generated examples, not official documents.
- Official scholarship/grant directory with source links, rule-based personalized suggestions and a Gemini consultation button; no awards or eligibility are guaranteed. Al-Xorazmiy is a search lead, not a confirmed national award.
- Education news/resource cards curated from official pages with original local SVG illustrations (not live news or official photographs).
- Interactive 3D-style CSS metric cards, academic profile and document cards. Statistics refresh every five seconds.
- External HEMIS, Mehnat, my.gov.uz and my.edu.uz links represent proposed integrations, not live connectors.
- The new detailed content and sample documents are primarily in Uzbek; the existing five-language navigation and AI language selection remain available.
- Seven automated tests cover backend functionality; real Gemini and full interactive browser validation remain manual.

### Upgrade from v2 (Windows)
Stop the v2 server (Ctrl+C). Extract v3 to a new directory, open its `murojaat-edu` folder in VS Code, copy your private `.env` from v2 into that folder, then run `npm.cmd ci` and `npm.cmd start`. Open http://localhost:3000 and refresh with Ctrl+F5. Sign out and back in to select a demo identity. Do not commit `.env`. Before public deployment set fresh private admin and demo codes and rotate any exposed API keys.

### Final visual update
The flying-envelope SVG is self-contained and animated, with a moving solution star and wind trails. Both portals share the branding and CSS hover effects. Motion respects the operating system reduced-motion preference. No new dependencies or environment variables are required.

### Sealed delivery logo revision
The envelope remains closed throughout the animation. Wind trails accompany arrival; the solution star appears after delivery and floats. The centered tagline has decorative rules on both sides. Existing hover effects remain.
