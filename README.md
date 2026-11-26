# Red Hound Studios

Fan-made films from Red Hound Studios, with a streaming-style catalogue, an in-page player and viewer ratings.

The whole site is `index.html` plus the `posters/` and `cast/` folders. Films, franchises and actors are listed in the `FILMS`, `FRANCHISES` and `ACTORS` arrays near the top of the script in `index.html`.

Every film, franchise and actor has its own page:

- `#/film/pool-shark-2` (the film's title in lowercase, with dashes)
- `#/franchise/ghostbusters`
- `#/actor/jordan`
- `#/actors` (everyone)

## Viewer ratings

A viewer can rate a film after watching at least 90% of it.

- **Films with an IMDb page** keep their IMDb score. The viewer average is shown next to it and doesn't change it.
- **Other films** start from the studio's score, which counts as 5 votes. Each viewer rating moves the score from there. For example, Pool Shark 2 starts at 2.7, and one 9/10 vote takes it to 3.8.

Right now ratings are saved only in each viewer's own browser. To share them so every viewer's vote counts for everyone, connect a free Firebase project:

1. Go to https://console.firebase.google.com and create a project. You can turn Google Analytics off.
2. Under **Build → Authentication → Sign-in method**, enable **Anonymous**.
3. Under **Build → Firestore Database**, create a database in production mode.
4. In Firestore's **Rules** tab, paste the contents of `firestore.rules` and publish them.
5. Under **Project settings → General → Your apps**, add a **Web** app and copy its `firebaseConfig` object.
6. In `firebase-config.js`, replace `null` with that object:

   ```js
   window.RH_FIREBASE = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     appId: "..."
   };
   ```

7. Under **Authentication → Settings → Authorized domains**, add `froodyofficial-maker.github.io`.

The Firebase web config isn't a secret, so it's fine to commit. The rules allow one rating per viewer per film, as a whole number from 1 to 10.
