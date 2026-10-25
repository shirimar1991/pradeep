# Krishna Cab Service — booking website

A responsive React + Vite booking website themed around the shop's interior reference: navy panels, warm wood, golden lighting accents, white surfaces and orange highlights. Brand name remains **Krishna Cab Service**.

## Features
- Responsive home, services, destinations and booking pages
- Customer booking enquiry form with required fields and date validation
- Indicative starting fares shown in Indian rupees (₹ INR); these are sample prices and must be verified by the business
- Supabase-backed booking submissions
- Admin control panel with booking statistics, search, status changes, details, fare quotes in INR and deletion
- Supabase Auth email/password sign-in for connected deployments
- Admin allow-list via `public.admin_users` and RLS policies in `supabase/schema.sql`
- Browser-local demo mode when Supabase is not configured

## Run locally
Requires Node.js 20+.

```bash
npm install
npm run dev
```

In demo mode, open **Control Panel** and use `KCS-demo-2026`. This is only for local demonstration. Do not use demo mode or the demo password for real customer data.

## Supabase setup
1. Create a Supabase project.
2. Run `supabase/schema.sql` in the Supabase SQL Editor.
3. Create your admin user in Supabase Dashboard → Authentication → Users, using an email/password you control.
4. Copy that user's UUID and run `insert into public.admin_users (user_id) values ('YOUR-AUTH-USER-UUID');` in SQL Editor, replacing the placeholder with the UUID.
5. Copy `.env.example` to `.env.local` and set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` (or publishable key).
6. Restart the Vite server.

The SQL only allows public users to create pending booking requests with no fare. Only allow-listed Supabase Auth users can view, update, quote fares or delete bookings. Never put the Supabase `service_role` key in a browser environment variable.

## GitHub
Create a repository, then run these commands from the project directory:

```bash
git init
git add .
git commit -m "Initial Krishna Cab Service booking website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

## Vercel
1. Import the GitHub repository into Vercel (Vite preset).
2. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` in Project Settings → Environment Variables.
3. Deploy and test a booking and an admin login.
4. Re-deploy after changing environment variables.

## Before launch
- The displayed starting prices are illustrative placeholders, not guaranteed quotes. Change `DEMO_RATES` in `src/main.jsx` to your real rates.
- Verify business phone, WhatsApp number, address and services.
- Add privacy, terms, cancellation/refund policies and consent text appropriate for your business.
- The booking form submits requests; it does not collect online payments. Fare is set by admin and confirmed with the customer.
- Run `npm run build` before deployment and test RLS policies using both a public session and your admin account.


## Netlify deployment

### Recommended: deploy from GitHub
1. Push this project folder to a GitHub repository.
2. In Netlify, choose **Add new site → Import an existing project** and select the repository.
3. Netlify reads `netlify.toml`: build command `npm run build`, publish directory `dist`, Node.js 20.
4. In **Site configuration → Environment variables**, add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` with your Supabase project values. Never add the Supabase service-role key.
5. Trigger a deploy. Test a customer booking and admin login after deployment.

### Important
This ZIP contains source code, not a prebuilt `dist` website. Do not drag this source ZIP directly into Netlify Drop. Import it through GitHub, or run `npm install` and `npm run build` locally and deploy the generated `dist` folder. Supabase must be configured for persistent live bookings and secure admin access; demo mode is for demonstration only.
