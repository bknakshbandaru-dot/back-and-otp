# Naksh AI

Naksh AI is a full-stack student-focused AI tutor with Firebase authentication, Firestore chat history, OpenAI streaming responses, study modes, image/PDF support, and a modern React interface.

## Features

- Email/password auth with email verification
- Google sign-in
- Persistent login with Firebase Auth
- Firestore-backed users, conversations, and messages
- Streaming AI answers from the backend
- Explain, Quiz, and Summary study modes
- Markdown answers with code block copy buttons
- Voice input using the browser speech API
- Image upload for visual explanation
- PDF upload with client-side text extraction and AI summarization
- Message actions for copy, regenerate, and delete
- Error boundary, retry logic, input validation, and rate limiting

## Project structure

- `client/`
  - `src/components`
  - `src/pages`
  - `src/hooks`
  - `src/utils`
  - `src/context`
  - `src/lib`
- `server/`
  - `src/routes`
  - `src/controllers`
  - `src/middleware`
  - `src/services`
  - `src/utils`

## Firestore collections

### `users/{uid}`

- `id`
- `email`
- `createdAt`
- `displayName`
- `emailVerified`
- `lastLoginAt`

### `conversations/{conversationId}`

- `id`
- `userId`
- `title`
- `createdAt`
- `updatedAt`
- `lastMessage`

### `conversations/{conversationId}/messages/{messageId}`

- `id`
- `conversationId`
- `role`
- `content`
- `timestamp`

## Environment setup

1. Copy `.env.example` to `.env`.
2. Fill in Firebase web config values for the client.
3. Fill in Firebase Admin values for the server.
4. Add your OpenAI API key.

Required values:

- `VITE_FIREBASE_API_KEY`
- `VITE_FIREBASE_AUTH_DOMAIN`
- `VITE_FIREBASE_PROJECT_ID`
- `VITE_FIREBASE_STORAGE_BUCKET`
- `VITE_FIREBASE_MESSAGING_SENDER_ID`
- `VITE_FIREBASE_APP_ID`
- `VITE_API_BASE_URL`
- `PORT`
- `CLIENT_URL`
- `OPENAI_API_KEY`
- `OPENAI_MODEL`
- `FIREBASE_PROJECT_ID`
- `FIREBASE_CLIENT_EMAIL`
- `FIREBASE_PRIVATE_KEY`

## Run locally

1. Install dependencies from the repo root:
   - `npm install`
2. Start the backend:
   - `npm run dev:server`
3. Start the frontend in another terminal:
   - `npm run dev:client`
4. Open `http://localhost:5173`

## Security notes

- The OpenAI API key stays on the server only.
- Chat routes require a Firebase ID token.
- Requests are validated with Zod.
- Chat requests are rate limited.
- Markdown is sanitized on the frontend.

## Backend API

### `POST /api/chat`

Streams a response using Server-Sent Events.

Body:

```json
{
  "message": "Explain photosynthesis simply",
  "history": [
    { "role": "user", "content": "What is photosynthesis?" }
  ],
  "mode": "explain",
  "attachments": []
}
```

The same route is also available at `POST /chat`.
