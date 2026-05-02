# Deployment Guide

## GitHub Setup

### 1. Create Repository

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit - Clarity Financial Intelligence Platform"

# Create repository on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/clarity.git
git branch -M main
git push -u origin main
```

### 2. Repository Settings

**Recommended settings:**
- Description: "AI-powered financial intelligence platform with tax optimization and FIRE planning"
- Website: (will be added after Vercel deployment)
- Topics: `fintech`, `saas`, `financial-planning`, `uk-tax`, `fire`, `stripe`, `chartjs`
- License: MIT

---

## Vercel Deployment

### Method 1: Vercel Dashboard (Recommended)

1. **Go to** [vercel.com](https://vercel.com) and sign in
2. **Click** "Add New" → "Project"
3. **Import** your GitHub repository
4. **Configure:**
   - Framework Preset: **Other**
   - Build Command: (leave empty)
   - Output Directory: (leave empty)
   - Install Command: (leave empty)
5. **Click** "Deploy"

**That's it!** Vercel will automatically:
- Deploy your site
- Generate a URL (e.g., `clarity-xyz.vercel.app`)
- Set up automatic deployments on git push

### Method 2: Vercel CLI

```bash
# Install Vercel CLI globally
npm i -g vercel

# Login to Vercel
vercel login

# Deploy
vercel

# Follow prompts:
# - Set up and deploy? Yes
# - Which scope? (select your account)
# - Link to existing project? No
# - What's your project's name? clarity
# - In which directory is your code? ./
# - Want to override settings? No

# Deploy to production
vercel --prod
```

---

## Post-Deployment Configuration

### 1. Add Stripe Keys

**⚠️ CRITICAL - Do this before accepting payments**

1. Get your Stripe publishable key:
   - Development: `pk_test_...` from [dashboard.stripe.com/test/apikeys](https://dashboard.stripe.com/test/apikeys)
   - Production: `pk_live_...` from [dashboard.stripe.com/apikeys](https://dashboard.stripe.com/apikeys)

2. Open `index.html` and find (around line 450):
   ```javascript
   const stripe = Stripe('pk_test_YOUR_STRIPE_PUBLISHABLE_KEY');
   ```

3. Replace with your key:
   ```javascript
   const stripe = Stripe('pk_live_YOUR_ACTUAL_KEY');
   ```

4. Commit and push:
   ```bash
   git add index.html
   git commit -m "Add Stripe production key"
   git push
   ```

Vercel will auto-deploy the update.

### 2. Custom Domain (Optional)

**In Vercel Dashboard:**
1. Go to your project → Settings → Domains
2. Add your domain (e.g., `clarity.app`)
3. Follow DNS instructions provided by Vercel
4. Wait for DNS propagation (up to 48 hours, usually 10 minutes)

**DNS Records to add at your registrar:**
```
Type: A
Name: @
Value: 76.76.21.21

Type: CNAME
Name: www
Value: cname.vercel-dns.com
```

### 3. Environment Variables (Future)

If you add backend functionality later:

**In Vercel Dashboard:**
1. Settings → Environment Variables
2. Add variables:
   - `STRIPE_SECRET_KEY` (for backend API)
   - `DATABASE_URL` (if adding persistence)
   - `JWT_SECRET` (if adding real auth)

---

## Monitoring & Analytics

### Enable Vercel Analytics

1. Go to project → Analytics
2. Enable Web Analytics (free)
3. Gets you:
   - Page views
   - Unique visitors
   - Top pages
   - Bounce rate
   - Performance metrics

### Add Google Analytics (Optional)

Add before closing `</head>` tag in `index.html`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

---

## CI/CD Pipeline (Automatic)

Vercel automatically sets up:

**On every `git push` to main:**
- ✅ Build verification
- ✅ Deploy to production
- ✅ Run performance checks
- ✅ Generate deployment URL

**On pull requests:**
- ✅ Deploy preview
- ✅ Unique preview URL
- ✅ Comment on PR with link

---

## Testing Deployment

### 1. Smoke Test Checklist

After deployment, test:

- [ ] Site loads without errors
- [ ] Login/signup works (any email, 8+ char password)
- [ ] Dashboard displays
- [ ] Charts render correctly
- [ ] Navigate to all 4 pages (Dashboard, Intelligence, Analyser, Plans)
- [ ] Add expense → verify dashboard updates
- [ ] Run AI analysis → insights appear
- [ ] Open Intelligence → all 5 tools load
- [ ] Settings → all 4 tabs work
- [ ] Payment modal opens (don't test actual payment in production without Stripe webhook)

### 2. Browser Testing

Test on:
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Mobile Safari (iPhone)
- [ ] Mobile Chrome (Android)

### 3. Performance Check

Use [PageSpeed Insights](https://pagespeed.web.dev/):
- Target: 90+ score
- Should get 95+ (single file, minimal dependencies)

---

## Troubleshooting

### Issue: Site shows 404

**Fix:** Check `vercel.json` exists and has correct routing:
```json
{
  "routes": [{"src": "/(.*)", "dest": "/index.html"}]
}
```

### Issue: Charts not rendering

**Fix:** Check browser console for CSP errors. Ensure CDN URLs are in CSP:
```html
<meta http-equiv="Content-Security-Policy" content="...script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net...">
```

### Issue: Stripe not loading

**Fix:** 
1. Check Stripe key is not `pk_test_YOUR_STRIPE_PUBLISHABLE_KEY`
2. Verify CSP allows `https://js.stripe.com`
3. Check browser console for errors

### Issue: Vercel build fails

**Fix:** This is a static site with zero build steps. If it fails:
1. Check `vercel.json` syntax
2. Ensure `index.html` exists in root
3. Remove any `package.json` if accidentally created

---

## Rollback

If something breaks:

### Vercel Dashboard
1. Go to Deployments
2. Find last working deployment
3. Click "..." → "Promote to Production"

### Git
```bash
git revert HEAD
git push
```

---

## Going Live Checklist

Before announcing publicly:

- [ ] Replace Stripe test key with live key
- [ ] Test actual card payment (use test card first)
- [ ] Set up Stripe webhook (if backend added)
- [ ] Add privacy policy page
- [ ] Add terms of service page
- [ ] Set up customer support email
- [ ] Enable Vercel Analytics
- [ ] Add custom domain
- [ ] Test on mobile devices
- [ ] Run security scan
- [ ] Set up error monitoring (Sentry, LogRocket, etc.)

---

**Your site is now live! 🚀**

Share it: `https://YOUR_PROJECT.vercel.app`
