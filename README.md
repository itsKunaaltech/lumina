# 💎 Lumina Jewels — E-Commerce Website

A complete, production-ready jewellery e-commerce website built with **Next.js 14**, **Supabase**, and **Razorpay**.

---

## 🗂 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 14 (App Router), TypeScript |
| Styling | Tailwind CSS, Framer Motion |
| Backend / DB | Supabase (PostgreSQL + Auth + Storage) |
| Payments | Razorpay |
| State | Zustand (cart persistence) |
| Deployment | Vercel |

---

## 🚀 Quick Start

### 1. Clone & Install

```bash
git clone <your-repo-url>
cd lumina-jewels
npm install
```

### 2. Set Up Supabase

1. Go to [supabase.com](https://supabase.com) and create a new project
2. In the SQL Editor, run the contents of `supabase/migrations/001_initial_schema.sql`
3. This creates all tables (profiles, products, orders, wishlists) + seeds 6 sample products

### 3. Set Up Razorpay

1. Create account at [razorpay.com](https://razorpay.com)
2. Go to **Settings → API Keys** → Generate Test API Key
3. Copy Key ID and Key Secret

### 4. Environment Variables

```bash
cp .env.local.example .env.local
```

Fill in your values:

```env
NEXT_PUBLIC_SUPABASE_URL=https://xxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGc...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGc...

RAZORPAY_KEY_ID=rzp_test_xxxx
RAZORPAY_KEY_SECRET=xxxx
NEXT_PUBLIC_RAZORPAY_KEY_ID=rzp_test_xxxx

NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 5. Run Dev Server

```bash
npm run dev
```

Visit `http://localhost:3000` 🎉

---

## 📁 Project Structure

```
lumina-jewels/
├── app/
│   ├── page.tsx              # Homepage (Hero, Categories, Featured)
│   ├── shop/page.tsx         # Shop listing with filters
│   ├── product/[id]/         # Product detail page
│   ├── cart/page.tsx         # Shopping cart
│   ├── checkout/page.tsx     # Checkout with Razorpay
│   ├── checkout/success/     # Order confirmation
│   ├── account/page.tsx      # User orders & profile
│   ├── auth/login/           # Sign in page
│   ├── auth/register/        # Sign up page
│   ├── admin/page.tsx        # Admin dashboard
│   └── api/
│       ├── razorpay/create-order/
│       ├── razorpay/verify-payment/
│       ├── auth/signout/
│       └── products/
├── components/
│   ├── layout/
│   │   ├── Navbar.tsx
│   │   └── Footer.tsx
│   └── shop/
│       ├── ProductCard.tsx
│       └── ProductDetail.tsx
├── lib/
│   ├── supabase.ts
│   ├── cart-store.ts         # Zustand cart
│   └── utils.ts
├── types/index.ts
└── supabase/migrations/      # DB schema + seed
```

---

## 🌐 Deploy to Vercel

### Option A — Vercel CLI

```bash
npm install -g vercel
vercel
```

Follow the prompts. When asked about environment variables, add them from your `.env.local`.

### Option B — GitHub + Vercel Dashboard

1. Push this project to a GitHub repo
2. Go to [vercel.com](https://vercel.com) → **New Project** → Import from GitHub
3. Add all environment variables in **Settings → Environment Variables**
4. Click **Deploy** ✅

### Production Razorpay

- Switch from `rzp_test_` to `rzp_live_` keys in Vercel env vars
- Add your live domain to Razorpay's allowed origins

---

## 👑 Admin Access

1. Create a user account via `/auth/register`
2. In Supabase Dashboard → Table Editor → `profiles`
3. Find your user → Set `is_admin = true`
4. Visit `/admin` to access the dashboard

---

## 🛍 Adding Products

**Via Admin Dashboard** (`/admin`):
- Click "+ ADD NEW" (links to `/admin/products/new`)

**Via Supabase Dashboard**:
- Go to Table Editor → `products` → Insert Row
- `images` field: add Supabase Storage URLs or any public image URLs

**Via Supabase Storage**:
1. Create a bucket named `product-images` (public)
2. Upload images
3. Copy the public URL into the `images` array

---

## 🎨 Customization

| What | Where |
|------|-------|
| Store name/address | `lib/utils.ts` → `STORE_INFO` |
| Colors & fonts | `tailwind.config.ts` + `app/globals.css` |
| Hero text | `app/page.tsx` |
| Categories | `app/page.tsx` → `CATEGORIES` array |
| Navigation | `components/layout/Navbar.tsx` |

---

## 💰 Business Notes (Selling this website)

This is a **white-label template** — to sell/reskin it:

1. Change `STORE_INFO` in `lib/utils.ts`
2. Update brand colors in `tailwind.config.ts`
3. Replace logo text in `Navbar.tsx`
4. Update font choices in `globals.css`
5. New Supabase project + Razorpay account for each client
6. Deploy to Vercel under client's domain

Each deployment takes ~30 minutes to configure.

---

## 📝 License

MIT — Use commercially, resell to clients, no attribution required.
