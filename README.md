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

Each user authorizes their own Spotify account. Playback controls require Spotify Premium and an active Spotify device.

## Airwave Meet

Airwave Meet creates a shareable room URL with listener presence, chat, and a shared now-playing signal. The current static build syncs between open tabs and windows on the same browser origin using `BroadcastChannel`; cross-device rooms require adding a realtime backend such as WebSockets or a hosted realtime database.
