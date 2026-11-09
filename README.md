# Kindred — AI companion MVP

**Kindred** is a mobile-friendly web app for conversations with AI characters. Choose from three distinct companions (Mira, Leo, and Nova), or create your own by selecting a name, personality traits, conversational tone, and visual style.

**Live demo:** _Add Netlify URL after deployment_

## What works

- Three ready-to-chat characters with distinct personalities.
- Custom character creation with color and expression choices.
- Live AI conversations powered by Google Gemini, with persona-specific instructions.
- Browser-based persistence for custom characters and full chat history.
- Conversation continuity: the latest 30 messages are provided as context for each AI response.
- Responsive interface with subtle animated SVG characters and reduced-motion support.

## Run locally

Requires Node.js and a Gemini API key.

```bash
npm install
npm install -g netlify-cli
cp .env.example .env
# Set GEMINI_API_KEY in .env (never commit this file)
netlify dev
```

Open the local URL shown by Netlify CLI (usually `http://localhost:8888`). Running `npm run dev` alone starts the UI but does not serve the AI function.

## Deploy to Netlify

1. Push the source to GitHub (do not commit `.env`).
2. Import the repository into Netlify. Build settings are defined in `netlify.toml`.
3. Set `GEMINI_API_KEY` in Netlify environment variables, available to Functions, then deploy or redeploy.
4. Open the HTTPS URL on a phone and verify character creation, chat, and persistence.

The Gemini API's free-tier availability and limits depend on Google's current policies and region.

## Product decisions and trade-offs

The goal was a working end-to-end companion experience within a **four-hour maximum**, not a feature-complete social platform.

- **React + Vite:** fast iteration and a lightweight, responsive frontend.
- **Netlify Functions:** keep the Gemini API key server-side without running a dedicated backend.
- **Gemini 3.5 Flash Lite:** real-time, persona-driven responses; the character's name, traits, description, and tone shape the system instruction.
- **`localStorage` instead of accounts/database:** zero-friction entry and reliable return visits in the same browser. The trade-off is no cross-device sync, and clearing site data removes the history.
- **Recent-context memory:** store the entire visible conversation locally, but send only the latest 30 messages to the model. This supports short-term continuity, not durable semantic memory of every fact ever mentioned.
- **Original SVG avatars:** distinctive, lightweight character visuals with subtle CSS motion; no image-generation service or external asset dependency.

## Validation

Manually tested: recalling details after a page refresh; preserving chats after closing and reopening the tab; keeping different characters' conversations separate; and correctly handling a user's correction of an earlier fact. These checks validate recent-context behavior, not unlimited long-term recall.

## What I would build next

If continuing beyond the MVP: optional accounts and cloud sync; user-controlled long-term memory summaries; stronger safety and moderation controls; and broader automated and mobile-device testing.

## Privacy and limitations

Chats and characters are stored in the current browser. Messages sent to the AI are processed by Google's Gemini API. Do not enter sensitive information in this demo. It is a prototype, not a production-ready service with a complete privacy, abuse-prevention, and account-security framework.
