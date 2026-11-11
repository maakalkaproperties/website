# Maa Kalkaji Properties - Hostinger Deployment Guide 🚀

Yeh guide aapko aapki Next.js + Supabase real estate website ko **Hostinger** par 10-15 minute me live karne ke steps deti hai.

---

## Method 1: Hostinger VPS (Sabse Best & Recommended for Next.js)

Next.js full-stack app (Server Actions, dynamic routes, API routes) ke liye Hostinger VPS sabse fast aur reliable hota hai.

### Step 1: VPS me Login karein (SSH)
Hostinger panel se apne VPS ka IP aur root password lein, aur terminal / PuTTY me run karein:
```bash
ssh root@YOUR_SERVER_IP
```

### Step 2: Node.js & Git Install karein
```bash
# System update
sudo apt update && sudo apt upgrade -y

# Node.js 20 LTS install
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs git nginx

# Verify versions
node -v   # v20.x.x
npm -v    # 10.x.x

# PM2 process manager install karein (Taki site 24/7 bina ruke chale)
sudo npm install -g pm2
```

### Step 3: Code Server par dalein
```bash
cd /var/www
git clone <YOUR_GIT_REPO_URL> maakalkaji
cd maakalkaji
npm install
```

### Step 4: Environment Variables (`.env`) configure karein
File create karein:
```bash
nano .env
```
Niche diye gaye variables paste karein:
```env
DATABASE_URL="postgresql://postgres:[ashishJI@9968]@db.ywfknwfemskzbidfxwav.supabase.co:5432/postgres?pgbouncer=true"
DIRECT_URL="postgresql://postgres:[ashishJI@9968]@db.ywfknwfemskzbidfxwav.supabase.co:5432/postgres"

NEXT_PUBLIC_SUPABASE_URL="https://ywfknwfemskzbidfxwav.supabase.co"
NEXT_PUBLIC_SUPABASE_ANON_KEY="sb_publishable_ji7zFedFb-LIfH-cHcSFMg__ezmiHfF"

NEXTAUTH_URL="https://yourdomain.com"
NEXTAUTH_SECRET="maakalkaji-super-secret-jwt-key-2026-ncr"

NEXT_PUBLIC_APP_URL="https://yourdomain.com"
NEXT_PUBLIC_AGENCY_NAME="Maa Kalkaji Properties"
NEXT_PUBLIC_AGENCY_PHONE="+91 98100 00000"
NEXT_PUBLIC_AGENCY_WHATSAPP="+919810000000"
NEXT_PUBLIC_AGENCY_EMAIL="info@maakalkajiproperties.com"
PORT=3000
NODE_ENV=production
```
*(Save karne ke liye `Ctrl + O`, enter, fir `Ctrl + X`)*

### Step 5: Database Push & Build
```bash
# Supabase sync
npx prisma generate
npx prisma db push

# Production Build
npm run build
```

### Step 6: App ko 24/7 background me start karein (PM2)
```bash
pm2 start npm --name "maakalkaji" -- start -- -p 3000
pm2 save
pm2 startup
```

### Step 7: Domain & Nginx Setup (Reverse Proxy + Free SSL)
```bash
sudo nano /etc/nginx/sites-available/maakalkaji
```
Paste karein (apna domain replace karein):
```nginx
server {
    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Nginx activate karein:
```bash
sudo ln -s /etc/nginx/sites-available/maakalkaji /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

Free SSL (HTTPS) lagayein:
```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

---

## Method 2: Hostinger hPanel (Shared / Cloud Node.js)
Agar aapke paas Hostinger Cloud Hosting hai aur hPanel me "Node.js" option hai:
1. **hPanel** me **Node.js** par jayein.
2. **Node.js version**: `20.x` select karein.
3. **Application root**: `public_html` ya `maakalkaji` folder.
4. **Application startup file**: `node_modules/next/dist/bin/next` aur arguments: `start`.
5. **Environment variables**: Supabase `DATABASE_URL`, `DIRECT_URL`, `NEXTAUTH_SECRET` add karein.
6. File Manager ya Git se files upload karke **Build** run karein.

---

## ⚡ Location Auto-Track feature notes:
Website me free location auto-track (GPS + OpenStreetMap Nominatim + IP detect) ready hai. Domain par HTTPS (SSL) active hote hi mobile browsers location permission mangkar user ke paas ki properties filter kar denge!
