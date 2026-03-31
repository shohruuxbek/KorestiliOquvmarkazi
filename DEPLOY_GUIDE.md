# 🚀 O'quv Markazi - Deploy Qo'llanma

## 📋 MUNDARIJA

1. [Tez Boshlash](#tez-boshlash)
2. [VPS Server Deploy](#vps-server-deploy)
3. [Render.com Deploy](#rendercom-deploy)
4. [Railway Deploy](#railway-deploy)
5. [Muammolarni Hal Qilish](#muammolarni-hal-qilish)

---

## ⚡ TEZ BOSHLASH (Localhost)

### Backend ishga tushirish:

```bash
cd backend
npm install
npm run start:prod
```

Backend: http://localhost:3000

### Frontend ishga tushirish:

```bash
cd frontend
npm install
npm run dev
```

Frontend: http://localhost:5173

---

## 🖥️ VPS SERVER DEPLOY

### 1-QADAM: Server Tayyorlash

**Ubuntu/Debian serverga SSH orqali ulaning:**
```bash
ssh root@server-ip-manzili
```

**Server yangilash:**
```bash
sudo apt update && sudo apt upgrade -y
```

### 2-QADAM: Git Clone

```bash
sudo apt install git -y
git clone <sizning-repozitoriyangiz-url> /var/www/oquv-markazi
cd /var/www/oquv-markazi
```

### 3-QADAM: Node.js O'rnatish

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version  # v20.x.x ko'rsatishi kerak
```

### 4-QADAM: PM2 Process Manager

```bash
sudo npm install -g pm2
pm2 --version
```

### 5-QADAM: Nginx Web Server

```bash
sudo apt install -y nginx
sudo systemctl status nginx
```

### 6-QADAM: Dependencies O'rnatish

**Backend:**
```bash
cd backend
npm install --production
```

**Frontend:**
```bash
cd ../frontend
npm install --production
```

### 7-QADAM: Environment Sozlash

**Backend .env.production:**
```bash
cd ../backend
nano .env.production
```

**Quyidagi ma'lumotlarni kiriting:**
```env
NODE_ENV=production
DATABASE_URL=sqlite://oquv_markazi.db
PORT=3000
HOST=0.0.0.0
JWT_SECRET=sizning-maxfiy-kalit-sozingiz
CORS_ORIGIN=*
```

**Frontend .env.production:**
```bash
cd ../frontend
nano .env.production
```

```env
VITE_API_URL=http://SERVER_IP_MANZILI:3000
```

> **Muhim:** `SERVER_IP_MANZILI` o'rniga haqiqiy server IP manzilini yozing!

### 8-QADAM: Build

**Backend:**
```bash
cd ../backend
npm run build
```

**Frontend:**
```bash
cd ../frontend
npm run build
```

### 9-QADAM: PM2 Ishga Tushirish

```bash
cd ..
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

PM2 startup buyrug'ini bajargandan so'ng, terminalda ko'rsatilgan buyruqni `sudo` bilan bajaring.

### 10-QADAM: Nginx Konfiguratsiyasi

**Konfiguratsiya faylini joylash:**
```bash
sudo cp nginx.conf /etc/nginx/sites-available/oquv-markazi
sudo ln -sf /etc/nginx/sites-available/oquv-markazi /etc/nginx/sites-enabled/
sudo rm -f /etc/nginx/sites-enabled/default
```

**Nginx test va qayta ishga tushirish:**
```bash
sudo nginx -t
sudo systemctl restart nginx
sudo systemctl enable nginx
```

### 11-QADAM: Firewall

```bash
sudo ufw allow 'Nginx Full'
sudo ufw allow 'OpenSSH'
echo "y" | sudo ufw enable
sudo ufw status
```

---

## ☁️ RENDER.COM DEPLOY

### Backend Deploy:

1. [render.com](https://render.com) da ro'yxatdan o'ting
2. **New +** → **Web Service**
3. Repository tanlang
4. **Sozlamalar:**
   - **Name:** oquv-backend
   - **Region:** Frankfurt (Europe)
   - **Branch:** main
   - **Root Directory:** `backend`
   - **Runtime:** Node
   - **Build Command:** `npm install && npm run build`
   - **Start Command:** `node dist/main.js`
   - **Instance Type:** Free

5. **Environment Variables:**
   ```
   NODE_ENV=production
   DATABASE_URL=sqlite://oquv_markazi.db
   PORT=3000
   JWT_SECRET=your-secret-key
   ```

### Frontend Deploy:

1. **New +** → **Static Site**
2. Repository tanlang
3. **Sozlamalar:**
   - **Name:** oquv-frontend
   - **Branch:** main
   - **Root Directory:** `frontend`
   - **Build Command:** `npm install && npm run build`
   - **Publish Directory:** `dist`

4. **Environment Variables:**
   ```
   VITE_API_URL=https://oquv-backend.onrender.com
   ```

---

## 🚂 RAILWAY.APP DEPLOY

### Backend:

1. [railway.app](https://railway.app) da ro'yxatdan o'ting
2. **New Project** → **Deploy from GitHub repo**
3. Repository tanlang
4. **Settings:**
   - **Root Directory:** `backend`
   - **Start Command:** `node dist/main.js`
   - **Build Command:** `npm install && npm run build`

5. **Variables:**
   ```
   NODE_ENV=production
   DATABASE_URL=sqlite://oquv_markazi.db
   PORT=3000
   ```

### Frontend:

1. Loyihada yana bir service qo'shing
2. **Service Type:** Empty Service
3. **Settings:**
   - **Root Directory:** `frontend`
   - **Build Command:** `npm install && npm run build`
   - **Start Command:** `npx serve dist`
   - **Port:** 5000

4. **Variables:**
   ```
   VITE_API_URL=<backend-railway-url>
   ```

---

## 🔧 MUAMMOLARNI HAL QILISH

### Backend ishga tushmayapti:

```bash
# PM2 logs ko'rish
pm2 logs oquv-backend

# PM2 restart
pm2 restart oquv-backend

# Port bandligini tekshirish
sudo lsof -i :3000
```

### Frontend API ga ulanmayapti:

1. `.env.production` faylida `VITE_API_URL` to'g'riligini tekshiring
2. Browser console'da CORS xatolarini tekshiring
3. Nginx konfiguratsiyasini qayta tekshiring

### Nginx xatolik:

```bash
# Nginx test
sudo nginx -t

# Nginx logs
sudo tail -f /var/log/nginx/error.log
sudo tail -f /var/log/nginx/access.log

# Nginx restart
sudo systemctl restart nginx
```

### Database muammosi:

```bash
# Database faylini tekshirish
ls -la backend/oquv_markazi.db

# Backup yaratish
cp backend/oquv_markazi.db backup_$(date +%Y%m%d).db
```

### PM2 avtomatik ishga tushmayapti:

```bash
# PM2 startup qayta
pm2 unstartup
pm2 startup
pm2 save
```

---

## 📊 FOYDALI BUYRUQLAR

### PM2:
```bash
pm2 status              # Barcha jarayonlar statusini ko'rish
pm2 logs                # Logs ko'rish
pm2 restart oquv-backend # Backend restart
pm2 stop oquv-backend   # Backend to'xtatish
pm2 delete oquv-backend # Backend o'chirish
pm2 monit               # Real-time monitoring
```

### Nginx:
```bash
sudo systemctl status nginx    # Status
sudo systemctl restart nginx   # Restart
sudo systemctl reload nginx    # Reload config
sudo nginx -t                  # Config test
```

### System:
```bash
sudo systemctl list-units --type=service  # Barcha servicelar
df -h                 # Disk joyi
free -h               # RAM holati
top                   # Jarayonlar monitori
```

---

## 🔒 XAVFSIZLIK MASALALARI

1. **JWT Secret** ni albatta o'zgartiring!
2. **Firewall** ni yoqing
3. **SSL sertifikat** o'rnating (Let's Encrypt)
4. **Database backup** qilishni unutmang
5. **Regular updates** qilib turing

### SSL Sertifikat (Let's Encrypt):

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d sizning-domeningiz.com
```

---

## 📞 YORDAM

Agar muammo yuzaga kelsa:

1. PM2 logs: `pm2 logs`
2. Nginx error logs: `sudo tail -f /var/log/nginx/error.log`
3. System logs: `journalctl -u nginx`

---

## ✅ DEPLOY CHECKLIST

- [ ] Server yangilangan
- [ ] Node.js o'rnatilgan (v20+)
- [ ] PM2 o'rnatilgan
- [ ] Nginx o'rnatilgan
- [ ] Backend dependencies o'rnatilgan
- [ ] Frontend dependencies o'rnatilgan
- [ ] .env.production fayllari to'ldirilgan
- [ ] Backend build qilingan
- [ ] Frontend build qilingan
- [ ] PM2 bilan backend ishga tushirilgan
- [ ] Nginx konfiguratsiyasi joylashtirilgan
- [ ] Firewall yoqilgan
- [ ] Sayt ochilmoqda ✅

---

**🎉 Tabriklaymiz! Loyihangiz deploy qilindi!**
