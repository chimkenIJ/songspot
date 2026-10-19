# songspot

A "name that tune" game made from **your own** music. Songspot plays a tiny slice of a song (0.1 seconds), and you try to guess it. Each skip plays more (0.5s, 2s, 5s, 15s), and the faster you guess, the more points you get.

**Play it here:** https://chimkenij.github.io/songspot/

You need songs in your pool before you can play. There are three ways to add them, and only the first one needs Spotify setup:

| Way | Setup needed |
| --- | --- |
| **Spotify** (pull in Liked Songs and your playlists) | A Spotify developer app. See below. |
| **CSV file** (for example an [Exportify](https://exportify.app) export) | None |
| **Paste list** (`Song - Artist`, one per line) | None |

To skip Spotify for now, go straight to the **CSV file** or **Paste list** tab. The audio clips come from Apple's free 30-second previews, so playing never needs a Spotify login.

---

## Connecting Spotify

The Spotify tab asks for a **Client ID**. A Client ID comes from a Spotify "developer app," and Spotify only lets an app log in people its owner has approved. You have two options:

- **Option A, use Isha's app (easiest):** Send Isha the email address you use for Spotify. Isha adds you to the app and sends you the Client ID.
- **Option B, make your own app (~5 minutes):** You need **Spotify Premium** for this. Spotify requires it for anyone who owns a developer app.

### Option A: use Isha's app

1. Send Isha the email address on your Spotify account. (Check it at spotify.com → Account → Edit profile.)
2. Wait until Isha says you've been added. Isha will also send you the **Client ID**.
3. Open the game, go to **Spotify**, paste the Client ID, and click **Connect Spotify**.

### Option B: make your own Spotify app

1. Go to **https://developer.spotify.com/dashboard** and log in with your Spotify account. The first time, you'll need to accept the developer terms.
2. Click **Create app** and fill in the form:
   - **App name:** anything, for example `songspot`
   - **App description:** anything, for example `song guessing game`
   - **Website:** leave it blank
   - **Redirect URIs:** paste `https://chimkenij.github.io/songspot/`, then click **Add**.
     (The game shows this same address in step 2 of its Spotify tab. If the two ever differ, use the one the game shows. It has to match **exactly**, including the `/` at the end.)
   - **Which API/SDKs are you planning to use?** Check **Web API**.
   - Tick the terms box and click **Save**.
3. On your new app's page, open **Settings** and copy the **Client ID**. You don't need the Client Secret, so leave it alone.
4. Open the game, go to **Spotify**, paste the Client ID, and click **Connect Spotify**.
5. Spotify asks you to allow access. Click **Agree**. You'll come back to the game with your playlists listed.

Your own account can always log in to your own app. To let a friend use it too, open the app in the dashboard → **Settings** → **User Management**, then add their name and Spotify email. A new app allows up to **5** people.

### Adding songs from Spotify

After you connect, tick **Liked Songs** and any playlists you want, then click **Add selected**.

Some playlists show up greyed out with a "not yours" label. This is a Spotify rule: an app can only read songs from playlists **you created or collaborate on**. To get songs from someone else's playlist, open it in Spotify, click **⋯ → Add to other playlist → New playlist**, and then add that copy instead.

---

## Troubleshooting

| What you see | What to do |
| --- | --- |
| **"INVALID_CLIENT: Invalid redirect URI"** on Spotify's page | The Redirect URI in your dashboard doesn't exactly match the address the game shows. Fix it under **Settings → Edit** and click **Save**. Then make sure you opened the game at that same address (not `.../index.html`). |
| **"User not registered in the Developer Dashboard"**, or a 403 error after logging in | The app owner hasn't added your Spotify email under **User Management**, or added a different email. |
| Login worked before but now fails | Spotify app logins stop working if the app owner's Premium lapses. They also expire after about 6 months. Click **Disconnect** and connect again. |
| "Could not find previews for your songs" | Apple has no preview for those songs (common for very new or obscure tracks), or your connection dropped. Add more songs and try again. |
| You want to start over | **Clear** removes your song pool. Everything is saved only in your own browser. |

---

## Privacy

There is no server. Your song list, settings, and Spotify login stay in your browser's local storage. The page only talks to Spotify (to read your playlists) and to Apple's iTunes search (to find the audio previews).

## Running it on your own computer

```sh
python3 -m http.server 8000
```

Then open **http://127.0.0.1:8000/**. For Spotify to work locally, also add `http://127.0.0.1:8000/` as a Redirect URI in your app. Spotify rejects `localhost`, so use `127.0.0.1`.
