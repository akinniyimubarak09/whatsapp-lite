# WhatsApp Lite

A responsive React + Vite messaging UI with original dark teal branding. Includes chat navigation, searchable demo conversations, responsive mobile chat view, theme switch, message composer, and Firebase email authentication / Firestore live-message wiring.

## 1. Run locally

Install Node.js 20 or newer, then run:

```bash
npm install
npm run dev
```

## 2. Enable real accounts and live messages

The interface works in demo mode without Firebase. For real cross-user messaging:

1. Create a project at https://console.firebase.google.com/
2. Add a Web app and copy its Firebase config.
3. In Firebase Authentication, enable **Email/Password**.
4. Create a Cloud Firestore database.
5. Add the environment values from `.env.example` to a local `.env` file (or configure them in Netlify).
6. Deploy, then add Firestore rules appropriate for your data model. Never leave production databases open to the public.

The current live-message query expects documents in `messages` with `members` (array of user IDs), `senderId`, `chatId`, `text`, and `createdAt` fields. For a complete production product, implement contact discovery, conversation creation/membership validation, robust Firestore security rules, moderation/reporting, rate limits, and file storage before inviting users. Do not use demo conversations as real private conversations.

## 3. Deploy to Netlify

### GitHub method (recommended)
1. Create a GitHub repository and upload/push this project.
2. Open https://app.netlify.com/ and choose **Add new site → Import an existing project**.
3. Connect GitHub and select the repository.
4. Build command: `npm run build`; publish directory: `dist` (also configured in `netlify.toml`).
5. Under **Site configuration → Environment variables**, add each `VITE_FIREBASE_*` value if using Firebase.
6. Deploy the site. After changing environment variables, trigger a new deploy.

### Manual deploy
Run `npm install` and `npm run build`, then drag the generated `dist` folder into Netlify's manual deploy area. Git-based deployment is better for ongoing updates.

## Important
- This is a starter application, not a finished secure WhatsApp replacement.
- Firebase web config is not a server secret, but database access must be protected by correct Firestore Security Rules.
- Calls, file sharing, push notifications, and end-to-end encryption are not implemented; the UI explains where these integrations can be added.
