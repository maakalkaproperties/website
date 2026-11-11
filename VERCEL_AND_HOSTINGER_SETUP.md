# 🚀 Maa Kalkaji Properties: Vercel + Hostinger Domain Guide

Yeh sabse smart aur zero-cost tarika hai jisme:
- **Hosting:** Vercel (100% FREE, Zero maintenance, Fast worldwide CDN)
- **Database:** Supabase (100% FREE, Already configured)
- **Domain:** Hostinger (Aapka khareeda hua domain)

---

## Step 1: Code ko GitHub par dalein (2 Minute)

Agar abhi tak GitHub repository nahi banayi:
1. [GitHub.com](https://github.com) par jayein aur **New Repository** banayein (e.g. `maa-kalkaji-properties`, Public ya Private).
2. Apne computer terminal me yeh commands chalayein:
```bash
cd C:\Users\LENOVO\.gemini\antigravity\scratch\delhi-ncr-real-estate
git init
git add .
git commit -m "Maa Kalkaji Properties with Supabase & GPS Auto-Track"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/maa-kalkaji-properties.git
git push -u origin main
```

---

## Step 2: Vercel par Free Deploy karein (2 Minute)

1. [Vercel.com](https://vercel.com) par jayein aur **Sign In with GitHub** karein (Free account).
2. **"Add New..."** -> **"Project"** par click karein.
3. Apni GitHub repository (`maa-kalkaji-properties`) ko **Import** karein.
4. **Environment Variables** section kholein aur niche diye gaye 5 variables paste karein:

| KEY | VALUE |
|---|---|
| `DATABASE_URL` | `postgresql://postgres:[ashishJI@9968]@db.ywfknwfemskzbidfxwav.supabase.co:5432/postgres?pgbouncer=true` |
| `DIRECT_URL` | `postgresql://postgres:[ashishJI@9968]@db.ywfknwfemskzbidfxwav.supabase.co:5432/postgres` |
| `NEXT_PUBLIC_SUPABASE_URL` | `https://ywfknwfemskzbidfxwav.supabase.co` |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | `sb_publishable_ji7zFedFb-LIfH-cHcSFMg__ezmiHfF` |
| `NEXTAUTH_SECRET` | `maakalkaji-super-secret-jwt-key-2026-ncr` |

5. **Deploy** button daba dein!
   * 1 minute me website live ho jayegi aur aapko ek free link mil jayega (e.g. `maa-kalkaji-properties.vercel.app`).

---

## Step 3: Hostinger ka Domain Vercel se Link karein (1 Minute)

1. **Vercel Project Dashboard** me:
   * **Settings** -> **Domains** par jayein.
   * Apna Hostinger wala domain type karein (e.g. `yourdomain.com`) aur **Add** karein.
2. Vercel aapko 2 DNS values dikhayega:
   * **A Record:** `76.76.21.21`
   * **CNAME Record:** `cname.vercel-dns.com` (for `www`)
3. **Hostinger Panel kholein:**
   * **hPanel** -> **Domains** -> Apne domain par click karein -> **DNS / Nameservers** me jayein.
   * **DNS Records** me:
     * Type: `A`, Name: `@`, Points to: `76.76.21.21`, TTL: `Default` -> Click **Add Record**.
     * Type: `CNAME`, Name: `www`, Points to: `cname.vercel-dns.com` -> Click **Add Record**.

---

## 🎉 Mubarak Ho!
Ab aapki website:
- Aapke Hostinger domain (`yourdomain.com`) par direct khulegi.
- Free SSL (Green Padlock 🔒) automatically lag jayega.
- VPS ka koi kharcha nahi, mahine ka zero bill!
