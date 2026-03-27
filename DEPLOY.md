# 🌿 GreenUSpeakUP — Deployment Guide
## Deploy to Vercel (Free) in 10 Minutes

---

## ✅ WHAT'S INCLUDED
- `index.html` — Complete single-file web app (React, no build step needed)
- `supabase_schema.sql` — Full database schema for Supabase
- `DEPLOY.md` — This guide

---

## 🚀 STEP 1 — Set Up Supabase (Free Database)

1. Go to **https://supabase.com** → Create a free account
2. Click **"New Project"** → Name it `greenuspeakup`
3. Set a strong database password → Click **Create Project**
4. Once ready, go to **SQL Editor** (left sidebar)
5. Paste the contents of `supabase_schema.sql` and click **Run**
6. Go to **Settings → API** and copy:
   - `Project URL` (looks like `https://xxxxx.supabase.co`)
   - `anon public` key (the long string under "Project API Keys")

---

## 🔑 STEP 2 — Add Your Supabase Credentials

Open `index.html` and find lines ~70-71:

```javascript
const SUPABASE_URL = 'https://YOUR_PROJECT.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY';
```

Replace with your actual values from Step 1.

> **Note:** The app ships with a full **localStorage demo mode** that works
> WITHOUT Supabase — great for testing locally. Once you add real credentials,
> it switches to the real database automatically.

---

## 🌐 STEP 3 — Deploy to Vercel

### Option A: Drag & Drop (Easiest)
1. Go to **https://vercel.com** → Sign in with GitHub
2. Go to **https://vercel.com/new**
3. Click **"Deploy without Git"**
4. Drag and drop your `index.html` file
5. Click **Deploy** → Done! ✅

### Option B: Via GitHub (Recommended for updates)
1. Create a new GitHub repository
2. Upload `index.html` to it
3. Go to Vercel → **"Add New Project"** → Import from GitHub
4. Select your repo → Click **Deploy**
5. Any future push to GitHub auto-deploys!

---

## 👑 STEP 4 — Set Up Your Admin Account

1. Open your live site
2. Register a new account using your admin email (e.g., `admin@youruniversity.edu`)
3. Go to your **Supabase Dashboard → Table Editor → profiles**
4. Find your user row → Change `role` from `user` to `admin`
5. Sign out and sign back in — you now have admin access!

---

## 🔒 STEP 5 — Supabase Authentication Settings

In Supabase Dashboard → **Authentication → Settings**:
- Disable email confirmation (for easier testing): Toggle off "Enable email confirmations"
- Or keep it on for production and set up your SMTP provider

---

## 📋 DEMO ACCOUNTS (localStorage mode only)
| Role    | Email                  | Password  |
|---------|------------------------|-----------|
| Admin   | admin@greenu.edu       | Admin@123 |
| Student | sarah@student.edu      | demo123   |

These only work in localStorage demo mode (without Supabase credentials).

---

## 🛠️ CUSTOMIZATION

### Change University Name
Search for `GreenUSpeakUP` in `index.html` and replace with your university name.

### Add More Categories
Find the `CATEGORIES` array (~line 270):
```javascript
const CATEGORIES = ['Academic', 'Facilities', ...];
```

### Change Colors
Find the `:root` CSS block (~line 20) and update:
```css
--green: #1a7a4a;        /* Primary color */
--accent: #f5c842;       /* Accent/highlight color */
```

---

## 🏗️ ARCHITECTURE

```
GreenUSpeakUP
├── Frontend: React (CDN, no build needed)
├── Database: Supabase (PostgreSQL + Auth + RLS)
├── Hosting: Vercel (free tier)
└── Storage: localStorage (demo) → Supabase (production)
```

**Why this stack for Vercel free tier?**
- No server-side code required (pure static)
- Supabase free tier: 500MB DB, 50K MAU, 2GB bandwidth
- Vercel free tier: unlimited static deploys, 100GB bandwidth/month

---

## 🐛 TROUBLESHOOTING

**"Auth error" on login** → Check your Supabase URL and anon key are correct

**Posts not saving** → Run the SQL schema again, ensure RLS policies are created

**Admin panel not showing** → Make sure your profile `role` = `'admin'` in Supabase

**Supabase CORS error** → Go to Supabase → Settings → API → Add your Vercel domain to allowed origins

---

## 📞 DATABASE TABLES OVERVIEW

| Table         | Purpose                              |
|---------------|--------------------------------------|
| profiles      | User profiles (extends auth.users)   |
| posts         | Student concerns/complaints          |
| likes         | Post likes (many-to-many)            |
| comments      | Post comments                        |
| notifications | User notification feed               |

---

Built with 💚 for student voices everywhere.
