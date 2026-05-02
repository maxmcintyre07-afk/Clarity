# Clarity — AI Financial Intelligence Platform

**Find money you're missing. Optimize your tax. Take control of your finances.**

A comprehensive financial planning SaaS built with vanilla JavaScript, Chart.js, and Stripe integration.

## Features

### 🎯 Core Functionality
- **AI Analyser** — Smart expense tracking with 14 preset categories
- **Real AI Insights** — Tax-aware recommendations with actionable next steps
- **Dashboard** — 4 key metrics + interactive charts
- **Intelligence Tools** — 5 advanced planning calculators
- **Plans & Billing** — Stripe payment integration (card only, production-ready)

### 🔥 Standout Features
- **Net Worth Projection** — 20-year compound growth visualization
- **FIRE Timeline Calculator** — Years until financial independence
- **Career Change Modeler** — "What if I quit at 40?" scenario planning
- **UK Tax Engine** — Marginal rate forecaster (Income Tax + NI + Student Loans)
- **Portfolio Optimizer** — ISA/SIPP/GIA efficiency checker

### 💼 Intelligence Tools
1. **Marginal Rate Forecaster** — UK 2024/25 tax calculations
2. **Asset Location Optimiser** — Tax-efficient account placement
3. **Strategy Sandbox** — Model business sales, retirement, property CGT
4. **Tax Loss Harvesting** — Track unrealized losses for CGT offsetting
5. **Future Asset Planner** — Target-based savings calculator

## Tech Stack

- **Frontend**: Vanilla JavaScript (ES6+)
- **Charts**: Chart.js 4.4.0
- **Payments**: Stripe.js v3
- **Styling**: Custom CSS with CSS variables
- **Fonts**: Inter (Google Fonts)
- **Deployment**: Vercel-ready static site

## Quick Start

### Local Development

1. Clone the repository:
```bash
git clone https://github.com/YOUR_USERNAME/clarity.git
cd clarity
```

2. Open `index.html` in your browser:
```bash
open index.html
# or
python3 -m http.server 8000
```

3. Navigate to `http://localhost:8000`

### Deploy to Vercel

1. Push to GitHub
2. Import project in Vercel dashboard
3. Deploy (zero configuration needed)

**Or use Vercel CLI:**
```bash
npm i -g vercel
vercel
```

## Configuration

### Stripe Setup (Required for Payments)

1. Get your Stripe publishable key from [Stripe Dashboard](https://dashboard.stripe.com)
2. Open `index.html`
3. Find line ~450: `const stripe = Stripe('pk_test_YOUR_STRIPE_PUBLISHABLE_KEY');`
4. Replace with your key: `const stripe = Stripe('pk_live_YOUR_KEY');`

### Backend Integration (Optional)

The payment flow currently shows "Connect your backend" for Apple/Google Pay. To enable:

1. Build a `/api/create-subscription` endpoint that:
   - Creates a Stripe Subscription
   - Returns `{clientSecret, error}`

2. Uncomment lines 480-520 in `index.html`
3. Card payments work immediately (no backend needed)

## Project Structure

```
clarity/
├── index.html          # Single-file application
├── README.md           # This file
└── .gitignore          # Git ignore rules
```

**Single-file architecture:** All HTML, CSS, and JavaScript in one file for simplicity and fast loading.

## User Guide

### Default Login
- Email: any email (demo mode)
- Password: any 8+ characters

### Sample Data
- Default income: £4,200/month
- Demo expenses included
- All calculations update live

### Settings
- **Financial Profile**: Income, age, portfolio, return rate
- **Tax & Retirement**: Student loan, pension %, SWR
- **Preferences**: Email notifications

## Key Calculations

### Net Worth Projection
```javascript
FV = StartingPortfolio × (1+r)^n + MonthlyContributions × ((1+r)^n - 1) / r
```

### FIRE Timeline
```javascript
TargetPortfolio = AnnualExpenses × (100 / SafeWithdrawalRate)
MonthsToFI = log(1 + (Target × r) / Monthly) / log(1 + r)
```

### Marginal Tax Rate
UK 2024/25 rates:
- Basic: 20% (£12,570 - £50,270)
- Higher: 40% (£50,270 - £125,140)
- Additional: 45% (£125,140+)
- NI: 12% up to £50,270, then 2%
- Student Loan: 9% above threshold

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## License

MIT License - see LICENSE file for details

## Support

For questions or issues, open a GitHub issue or contact support@clarity.app

---

**Built with focus on clarity over cleverness. Simple beats complex.**
