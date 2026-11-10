# 🌸 Tara: your gentle health companion

Tara is a cute, private-by-design period, mood, sleep and wellness tracker for the browser and phone (installable as an app). It has animated mood stickers, a cycle wheel, a calendar with reminders, a journal and personal wellness suggestions.

**Live app:** https://tara-137-5.web.app

---

## Screenshots

| Login | Home: cycle wheel | Home: sticker, journal, calendar |
|:--:|:--:|:--:|
| ![Login](screenshots/01-login.png) | ![Home wheel](screenshots/02-home-wheel.png) | ![Home sticker](screenshots/03-home-sticker-journal.png) |

| Suggestions | Mood stickers | Calendar |
|:--:|:--:|:--:|
| ![Suggestions](screenshots/04-home-suggestions.png) | ![Moods](screenshots/05-mood-stickers.png) | ![Calendar](screenshots/06-calendar.png) |

| Add event or reminder | Journal | Care tips |
|:--:|:--:|:--:|
| ![Add event](screenshots/07-calendar-add-event.png) | ![Journal](screenshots/08-journal.png) | ![Care](screenshots/09-care.png) |

| Sleep log | Water reminder | Walk reminder |
|:--:|:--:|:--:|
| ![Sleep](screenshots/10-sleep-log.png) | ![Water](screenshots/11-reminder-water.png) | ![Walk](screenshots/12-reminder-walk.png) |

| Stretch reminder | Event alert |
|:--:|:--:|
| ![Stretch](screenshots/13-reminder-stretch.png) | ![Event alert](screenshots/14-event-alert.png) |

*Screenshots use sample demo data.*

---

## Features

- **Cycle wheel**: numbered day ring coloured by phase (period, follicular, fertile, ovulation, luteal) with today highlighted, plus predictions for the next period and fertile window.
- **16 mood stickers**: Happy, Cute, Excited, Calm, Angry, Surprised, Sad, Shy, Sleepy, Tired, Thinking, Love, Playful, Cool, Confused, Grateful. Each one is animated and comes with a gentle tip.
- **Calendar**: month view with period days, predicted days and fertile window, plus your own **events and reminders** with alerts (at the time, 10 min, 1 hour or 1 day before) and repeats (daily, weekly, monthly, yearly).
- **Period log**: mark start and end, flow, symptoms and period length.
- **Journal**: private entries with an auto-attached mood and a mood-based writing prompt; edit and delete anytime.
- **Sleep**: log hours from the Home tile. Tara remembers your usual sleep until you change or reset it (falls back to your bedtime plan).
- **Tara's suggestions**: personal tips based on your recent sleep, symptoms, flow, cycle phase and water intake.
- **Reminders** with animated sticker pop-ups: water, walks, stretch and bedtime.
- **Installable** on Android and iPhone (PWA) with offline support for the app shell.

## Tech stack

- Front end: plain **HTML, CSS and JavaScript**. No framework and no build step.
- Login and database: **Firebase Authentication** (Google) and **Cloud Firestore**.
- Hosting: **Firebase Hosting** (free Spark plan).

## Privacy: what is stored

- Tara asks people to sign in with Google. It receives their **name and email** for login.
- Their entries (moods, period log, journal, events, sleep and so on) are saved to **their own private record** in Firestore so they follow them to a new phone. A copy is also kept in the browser on their device.
- Firestore rules allow each person to read and write **only their own record** (`firestore.rules`).
- There are **no ads, no analytics and no tracking**. Nothing is sold or shared.
- Settings has **Delete all my data**, which clears the device copy and the cloud copy.
- Note for the project owner: as admin of the Firebase project you can technically view the database in the console. Please never look at users' data.
- Tara is a wellness guide. **Predictions and tips are estimates and not medical advice.**

## Run it locally

Needs Node.js 16 or newer.

```
npm start
```

Open http://localhost:3000. With `TARA_FIREBASE` left as `null` in `public/firebase-config.js`, the app runs in local-only device mode (no login, data stays in the browser).

## Set up Firebase and deploy

1. Create a project at https://console.firebase.google.com
2. **Authentication**: Get started, enable **Google** and save.
3. **Firestore Database**: Create database (Production mode).
4. **Project settings**: add a **Web app** and copy its config.
5. Paste the config into `public/firebase-config.js` as `window.TARA_FIREBASE = { ... };`
6. In the project folder run:
   ```
   npm install -g firebase-tools
   firebase login
   firebase deploy
   ```
7. In Authentication, Settings, **Authorized domains**, make sure your `*.web.app` domain is listed.

To update the live app after changes, run `firebase deploy` again. A step-by-step version for beginners is in `HOW-TO-SHARE.txt`.

## Install on a phone

- **Android:** open the link in Chrome, tap the ⋮ menu, then **Install app**.
- **iPhone:** open the link in Safari, tap **Share**, then **Add to Home Screen**.

## Project structure

```
tara/
├─ firebase.json, .firebaserc, firestore.rules   Firebase hosting and database rules
├─ server.js, package.json                       tiny local test server
├─ screenshots/                                  images used in this README
└─ public/
   ├─ index.html, style.css, app.js              the whole app
   ├─ firebase-config.js                         your Firebase web config
   ├─ sw.js, manifest.json                       offline support and install info
   ├─ icon-192.png, icon-512.png, apple-touch-icon.png, favicon.png
   └─ img/                                       logo and sticker artwork
```

## Customising

- **Stickers and logo**: replace the files in `public/img/` (keep the same names). Mood stickers are named after their mood (for example `happy.webp`).
- **Moods, tips and prompts**: edit `MOODS`, `ACT` and `JPROMPT` near the top of `public/app.js`.
- **Colours**: the CSS variables at the top of `public/style.css`.
- After changing files, bump the cache name in `public/sw.js` (for example `tara-v6` to `tara-v7`) so installed apps pick up the update.

## Known limits

- Event and reminder alerts pop up while Tara is open. A fully closed app cannot send alerts without a separate push-notification server.
- All of a user's data lives in one Firestore document (1 MB limit, which is thousands of short entries).
- Sticker artwork is supplied by the project owner. Make sure you have the right to use it publicly.

---

Made with 💗 by VR
