# ROME CRE — PM Task Calendar

A shared monthly property management task calendar for the ROME team. Track mortgage payments, ground lease payments, owner distributions, tenant emails, variance reports, and every other recurring PM task — with check-off tracking, team attribution, and a full history archive.

## Quick Start (works immediately)

1. Open `index.html` in any browser — it works right away using local storage
2. Select your name from the dropdown
3. Click any day to see and check off tasks
4. Add, edit, or remove tasks via the UI

**That's it for single-user.** To share with the whole team, continue to the GitHub + Firebase setup below.

---

## Deploy to GitHub Pages (share with the team)

### Step 1: Create a GitHub repo

1. Go to [github.com/new](https://github.com/new)
2. Name it `rome-pm-calendar` (or whatever you want)
3. Set it to **Private** (only team members with access can view)
4. Click **Create repository**

### Step 2: Push the files

Open Terminal on your Mac and run:

```bash
cd ~/Downloads/CALENDAR\ TO\ DO\ LIST/rome-pm-calendar
git init
git add .
git commit -m "Initial PM calendar"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/rome-pm-calendar.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

### Step 3: Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under "Source", select **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Click **Save**
5. Wait ~60 seconds. Your calendar is now live at: `https://YOUR_USERNAME.github.io/rome-pm-calendar/`

Share that URL with the team.

---

## Set Up Firebase (so everyone shares the same data)

Without Firebase, each person's browser tracks tasks independently. Firebase syncs everything in real-time — when Sam checks off the mortgage payment, everyone sees it instantly.

### Step 1: Create a Firebase project (5 minutes, free)

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Create a project** (or Add project)
3. Name it `rome-pm-calendar`
4. Disable Google Analytics (not needed) → **Create Project**

### Step 2: Add a web app

1. On the project overview page, click the **web icon** (`</>`)
2. Nickname: `pm-calendar`
3. Skip Firebase Hosting (you're using GitHub Pages)
4. Click **Register app**
5. You'll see a config object like this — **copy it**:

```js
{
  apiKey: "AIzaSy...",
  authDomain: "rome-pm-calendar.firebaseapp.com",
  projectId: "rome-pm-calendar",
  storageBucket: "rome-pm-calendar.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
}
```

### Step 3: Enable Firestore

1. In the Firebase console sidebar, click **Firestore Database**
2. Click **Create database**
3. Choose **Start in test mode** (you can tighten rules later)
4. Pick the closest region (e.g., `us-west1` for Sacramento)
5. Click **Enable**

### Step 4: Paste the config into the calendar

1. Open the PM Calendar in your browser
2. Click the **gear icon** (top right)
3. Paste the Firebase config JSON into the text box
4. Click **Save**

Done. The calendar now syncs across every browser that has the same config. When you or Sam or Chase checks off a task, everyone sees it in real-time.

### Optional: Lock down Firestore rules

Once everything works, go to Firestore → **Rules** and replace with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

This is open access (fine for an internal tool behind a private GitHub Pages URL). For tighter security, you can add Firebase Authentication later.

---

## Default Tasks Included

| Day | Task | Category |
|-----|------|----------|
| 1st | Bank Reconciliations (all properties) | Financial |
| 1st | Monthly Financial File Organization | Admin |
| 1st-5th | AP Invoice Entry (Yardi) | Financial |
| 1st-5th | Review Prior Month Financials | Reporting |
| 2nd Monday | 1st Round Tenant Balance Emails | Operations |
| 10th | BRK Retail Sales — Collect & Enter | Reporting |
| 10th | Financial Package Cover Letters | Reporting |
| 15th | Budget vs. Actual Variance Reports | Reporting |
| 15th | Send Variance Summary to Sam | Reporting |
| 3rd Monday | 2nd Round Tenant Balance Emails | Operations |
| 20th | Mortgage Payment Reminder — 2901 K St | Financial |
| 4th Friday | ROME Brokerage Monthly Meeting | Admin |
| 25th | Ground Lease Payment | Financial |
| 27th | Mortgage Payment — 2901 K St | Financial |
| Last biz day | Owner Distributions | Financial |
| Last biz day | Month-End Close | Admin |

All tasks are fully editable via the UI — add, edit, delete, change schedules.

---

## Features

- **Monthly calendar grid** with task indicators on each day
- **Click any day** to see tasks, check them off, see who completed what
- **Team member selector** — tracks who did what
- **Category filters** — Financial, Reporting, Operations, Admin
- **History view** — archive of every month's completion rate
- **Add/edit/delete tasks** with flexible scheduling (fixed day, Nth weekday, last business day, date range)
- **Firebase real-time sync** — optional, for team sharing
- **Works offline** — localStorage fallback when Firebase isn't connected
- **Mobile responsive** — works on phones and tablets
