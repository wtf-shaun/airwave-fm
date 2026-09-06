# Airwave FM

A static Spotify radio experience for Vercel. Each visitor signs into their own Spotify account using Authorization Code with PKCE.

## Deploy to Vercel

1. In `app.js`, confirm `CLIENT_ID` contains your Spotify Client ID. A Client Secret is not needed.
2. Deploy this `airwave-fm` folder as the Vercel project root.
3. Add your deployed URL to the Spotify Developer Dashboard Redirect URIs, for example:

       https://your-project.vercel.app/

4. Open the deployed URL and choose **Tune into Spotify**.

Use **Other** as the Vercel framework preset, leave the build command blank, and use `.` as the output directory.

## Local testing

From this folder, run:

    python -m http.server 3000

Then open `http://localhost:3000/`. Add this exact local URL to Spotify Redirect URIs:

    http://localhost:3000/

Each user authorizes their own Spotify account. Playback controls require Spotify Premium and an active Spotify device. The app requests `streaming`, `user-read-email`, `user-read-private`, `user-modify-playback-state`, and `user-read-playback-state`.

## Airwave Meet

Airwave Meet creates a shareable room URL with listener presence, chat, and a shared now-playing signal. Each participant authorizes their own Spotify account when they want synchronized playback. PeerJS provides the browser-to-browser room connection; deploy the app over HTTPS for cross-computer networking, while `BroadcastChannel` remains as the local-tab fallback.

### Camera rooms

Inside a room, choose **Join camera** and allow camera/microphone access. Other participants appear in the live video grid, and each person can mute their microphone or turn their camera off. Camera access requires an HTTPS deployment or `localhost`; it will usually be blocked when opening `index.html` directly with a `file://` URL.

Guests can optionally connect their own Spotify account and choose **Sync to my Spotify**. Airwave sends the host's track URI and estimated position; each guest's Spotify app then starts that song locally. Spotify Premium and an active playback device are required, and the app never relays the host's audio.

The room also includes Spotify Web Playback SDK support. After connecting Spotify, choose a genre and press **Play genre** to play a matching track inside the Airwave page. Track selection uses Spotify Search with a randomized result offset and a per-session genre cache; it does not use the deprecated Recommendations API. Browser playback requires Spotify Premium, HTTPS, and the user's click to start playback.

### Production security note

This repository is currently a static Vercel build. Access and refresh tokens are kept in the current browser session so the demo can run without a backend. Production deployment should move OAuth token exchange and refresh into a server/API route or encrypted httpOnly cookie, and replace PeerJS room signaling with an authenticated realtime provider. Tokens must remain isolated per user session and must never be shared as room state.
