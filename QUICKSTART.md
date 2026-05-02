# Quick Start — 5 Minutes to Live

## Step 1: GitHub (2 minutes)

```bash
# In your terminal, navigate to where you want the project
cd ~/projects

# Create new directory
mkdir clarity
cd clarity

# Download the files (you'll copy them from /mnt/user-data/outputs/)
# Copy: index.html, README.md, LICENSE, .gitignore, vercel.json, DEPLOYMENT.md

# Initialize git
git init
git add .
git commit -m "Initial commit"

# Create GitHub repo at github.com/new
# Then connect:
git remote add origin https://github.com/YOUR_USERNAME/clarity.git
git branch -M main
git push -u origin main
```

## Step 2: Vercel (3 minutes)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click "Import" next to your `clarity` repository
3. Click "Deploy" (no configuration needed)
4. Wait 30 seconds
5. Done! ✅

**Your URL:** `https://clarity-XXXXX.vercel.app`

## Step 3: Test (30 seconds)

1. Open your Vercel URL
2. Click "Create account"
3. Enter any email + password (8+ chars)
4. You're in!

---

## Optional: Add Stripe (for real payments)

1. Get key from [dashboard.stripe.com/test/apikeys](https://dashboard.stripe.com/test/apikeys)
2. Open `index.html`, find line ~450
3. Replace `'pk_test_YOUR_STRIPE_PUBLISHABLE_KEY'` with your actual key
4. Commit and push:
   ```bash
   git add index.html
   git commit -m "Add Stripe key"
   git push
   ```

Vercel auto-deploys in 30 seconds.

---

## What You Have Now

✅ **Live SaaS app** at your Vercel URL  
✅ **Auto-deploys** on every git push  
✅ **Preview URLs** for pull requests  
✅ **SSL certificate** (automatic HTTPS)  
✅ **Global CDN** (fast everywhere)  

## What Works Out of the Box

- Login/signup (demo mode, any email works)
- Dashboard with 4 stats + 3 charts
- AI Analyser with 14 expense categories
- 5 Intelligence tools (tax, portfolio, FIRE, etc.)
- Net worth projection (20 years)
- Settings (4 comprehensive tabs)
- Payment modal (Stripe integration ready)

## What to Do Next

**Today:**
1. Share the URL with 5 people
2. Get feedback
3. Fix any bugs

**This Week:**
1. Add custom domain (Settings → Domains in Vercel)
2. Set up Vercel Analytics (free, one click)
3. Replace Stripe test key with live key

**This Month:**
1. Build backend API for real payments
2. Add user authentication (Firebase/Supabase)
3. Connect database for persistence
4. Add email notifications
5. Launch marketing site

---

**That's it. You're live.**

Questions? Check [DEPLOYMENT.md](DEPLOYMENT.md) for detailed guide.
