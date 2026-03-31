# 🚀 Oracle Cloud Free Tier - To'liq Deploy Qo'llanma

## 📋 NIMA UCHUN ORACLE CLOUD?

✅ **2 ta VM instance** (ARM yoki AMD)  
✅ **24GB RAM** jami (har biriga 12GB)  
✅ **2 OCPU** (4 OCPU threads)  
✅ **200GB disk**  
✅ **Cheksiz bandwidth**  
✅ **Hech qachon to'lov yo'q!** (Always Free)

---

## 1️⃣ RO'YXATDAN O'TISH

### Qadam 1: Oracle Cloud saytiga kiring
```
https://www.oracle.com/cloud/free/
```

### Qadam 2: "Start for free" tugmasini bosing

### Qadam 3: Ma'lumotlarni kiriting

**Kerakli ma'lumotlar:**
- ✅ Email address (haqiqiy email!)
- ✅ First name & Last name
- ✅ Country/Region (O'zbekiston tanlang)
- ✅ Mobile phone number (+998 bilan)
- ✅ Credit/Debit card (faqat tasdiqlash uchun, pul yechilmaydi!)

### Qadam 4: Telefon raqamni tasdiqlash
- SMS kod keladi
- Kodni kiriting

### Qadam 5: Karta ma'lumotlari
- Visa/Mastercard raqami
- Faqat $1 ushlab turadi va qaytaradi
- **Hech qanday pul yechilmaydi!**

### Qadam 6: Email tasdiqlash
- Emailga link keladi
- Linkni oching

### Qadam 7: Login
```
https://cloud.oracle.com
```
- Email va parol kiriting

---

## 2️⃣ SSH KALIT YARATISH

### Windows uchun (PuTTYgen):

**1. PuTTYgen yuklab oling:**
```
https://www.puttygen.com/
```

**2. PuTTYgen ni oching:**
- Algorithm: **RSA**
- Number of bits: **2048**
- "Generate" tugmasini bosing
- Sichqonchani harakatlantiring (randomness uchun)

**3. Kalitni saqlang:**
- "Save private key" → `oracle_key.ppk`
- **Muhim:** Public key ni nusxalab oling (yuqoridagi oynada)

### Linux/Mac uchun (Terminal):

```bash
ssh-keygen -t rsa -b 2048 -f oracle_key
```

**Public key ni ko'rish:**
```bash
cat oracle_key.pub
```

**Natija:**
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ... oracle_key
```

Bu satrni nusxalab oling!

---

## 3️⃣ VM INSTANCE YARATISH

### Qadam 1: Oracle Cloud Dashboard

1. Login qiling: `https://cloud.oracle.com`
2. **"Create a VM instance"** tugmasini bosing

### Qadam 2: Instance Configuration

**Image and Shape:**
- **Image:** Ubuntu 22.04 Minimal
- **Shape:** VM.Standard.A1.Flex (ARM)
- **Networking:** Virtual cloud network (avtomatik yaratiladi)

**O'lchamni tanlash:**
```
✅ Operating mode: Always Free
✅ OCPU count: 2
✅ Memory (GB): 12
```

### Qadam 3: SSH Kalit Qo'shish

**Add SSH keys:**
- "Upload public key files" ni tanlang
- Yaratgan public key faylingizni yuklang (`oracle_key.pub`)
- Yoki public key matnini paste qiling

### Qadam 4: Boot Volume

```
✅ Use default boot volume size
✅ Size: 50GB (bepul)
```

### Qadam 5: Networking

```
✅ Assign a public IPv4 address
✅ Firewall ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)
```

### Qadam 6: Create

- **"Create"** tugmasini bosing
- 2-5 daqiqa kutiladi
- Instance tayyor!

### Qadam 7: IP Manzilni Ko'chirish

Instance yaratilgandan keyin:
- **Public IP address** ni ko'chirib oling
- Masalan: `129.146.89.123`

---

## 4️⃣ SERVERGA ULANISH

### Windows (PuTTY):

**1. PuTTY yuklab oling:**
```
https://www.putty.org/
```

**2. PuTTY Configuration:**
- Host Name: `opc@<server-ip>`
- Port: `22`
- Connection type: `SSH`

**3. SSH Auth:**
- Connection → SSH → Auth
- Private key file: `oracle_key.ppk`

**4. Open:**
- Terminal ochiladi
- Username: `opc`

### Linux/Mac:

```bash
ssh -i oracle_key opc@<server-ip>
```

**Masalan:**
```bash
ssh -i oracle_key opc@129.146.89.123
```

**Birinchi marta ulanish:**
```
Are you sure you want to continue connecting (yes/no)? yes
```

---

## 5️⃣ SERVER SOZLASH

### Qadam 1: Server yangilash

```bash
sudo apt update
sudo apt upgrade -y
```

### Qadam 2: Node.js o'rnatish

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version  # v20.x.x bo'lishi kerak
npm --version   # 10.x.x bo'lishi kerak
```

### Qadam 3: Git o'rnatish

```bash
sudo apt install -y git
git --version
```

### Qadam 4: PM2 o'rnatish

```bash
sudo npm install -g pm2
pm2 --version
```

### Qadam 5: Nginx o'rnatish

```bash
sudo apt install -y nginx
sudo systemctl status nginx
```

---

## 6️⃣ LOYIHANI SERVERGA YUKLASH

### Variant A: Git Clone (Tavsiya)

```bash
# GitHub repo'ngizdan clone qiling
cd /home/opc
git clone https://github.com/sizning-username/oquv-markazi.git
cd oquv-markazi
```

### Variant B: SCP bilan Yuklash

**Local kompyuteringizda:**
```bash
scp -i oracle_key -r ./* opc@<server-ip>:/home/opc/oquv-markazi
```

### Variant C: FileZilla

1. FileZilla yuklab oling
2. SFTP protocol
3. Host: `<server-ip>`
4. Username: `opc`
5. Key file: `oracle_key.ppk`
6. Fayllarni sudrab o'tkazing

---

## 7️⃣ BACKEND SOZLASH

```bash
cd /home/opc/oquv-markazi/backend

# Dependencies
npm install --production

# .env.production yaratish
nano .env.production
```

**.env.production fayli:**
```env
NODE_ENV=production
DATABASE_URL=sqlite://oquv_markazi.db
PORT=3000
HOST=0.0.0.0
JWT_SECRET=sizning-maxfiy-kalit-sozingiz-12345
CORS_ORIGIN=*
LOG_LEVEL=info
```

**Build:**
```bash
npm run build
```

---

## 8️⃣ FRONTEND SOZLASH

```bash
cd /home/opc/oquv-markazi/frontend

# Dependencies
npm install --production

# .env.production yaratish
nano .env.production
```

**.env.production fayli:**
```env
VITE_API_URL=http://<SERVER_IP>:3000
```

**Muhim:** `<SERVER_IP>` o'rniga server IP manzilini yozing!

**Build:**
```bash
npm run build
```

---

## 9️⃣ PM2 BILAN ISHGA TUSHIRISH

```bash
cd /home/opc/oquv-markazi

# PM2 bilan ishga tushirish
pm2 start ecosystem.config.js

# Status tekshirish
pm2 status

# Logs ko'rish
pm2 logs

# Auto-start sozlash
pm2 startup
pm2 save
```

**PM2 startup buyrug'ini bajargandan keyin:**
Terminal sizga bir buyruq beradi, uni `sudo` bilan bajaring:

```bash
sudo env PATH=$PATH:/usr/bin pm2 startup systemd -u opc --hp /home/opc
```

---

## 🔟 NGINX KONFIGURATSIYASI

### Nginx config faylini joylash:

```bash
sudo cp /home/opc/oquv-markazi/nginx.conf /etc/nginx/sites-available/oquv-markazi
sudo ln -sf /etc/nginx/sites-available/oquv-markazi /etc/nginx/sites-enabled/
sudo rm -f /etc/nginx/sites-enabled/default
```

### Nginx test:

```bash
sudo nginx -t
```

Agar "successful" deb chiqsa:

```bash
sudo systemctl restart nginx
sudo systemctl enable nginx
```

### Firewall ochish:

```bash
sudo ufw allow 'Nginx Full'
sudo ufw allow 'OpenSSH'
echo "y" | sudo ufw enable
sudo ufw status
```

---

## 1️⃣1️⃣ ORACLE CLOUD FIREWALL

Oracle Cloud dashboard'da firewall ochish kerak:

1. Oracle Cloud Console → Networking → Virtual Cloud Networks
2. VCN tanlang
3. Security Lists → Default Security List
4. Ingress Rules qo'shing:

**Port 80 (HTTP):**
```
Source CIDR: 0.0.0.0/0
Destination Port Range: 80
Description: HTTP
```

**Port 443 (HTTPS):**
```
Source CIDR: 0.0.0.0/0
Destination Port Range: 443
Description: HTTPS
```

**Save** bosing!

---

## 1️⃣2️⃣ TEKSHIRISH

### Saytni oching:

```
http://<SERVER_IP>
```

Masalan: `http://129.146.89.123`

### Backend API test:

```bash
curl http://<SERVER_IP>/api/students
```

### PM2 status:

```bash
pm2 status
```

### Nginx status:

```bash
sudo systemctl status nginx
```

---

## 🔧 MUAMMOLARNI HAL QILISH

### Agar sayt ochilmasa:

**1. Oracle Cloud Firewall tekshiring:**
- VCN → Security Lists → Ingress Rules
- Port 80 va 443 ochiqmi?

**2. Server Firewall:**
```bash
sudo ufw status
```

**3. Nginx logs:**
```bash
sudo tail -f /var/log/nginx/error.log
```

### Agar backend ishlamasa:

**PM2 logs:**
```bash
pm2 logs oquv-backend
```

**Port bandligi:**
```bash
sudo lsof -i :3000
```

### Agar SSH ulanmasa:

```bash
# Debug mode
ssh -vvv -i oracle_key opc@<server-ip>
```

---

## 📊 FOYDALI BUYRUQLAR

### PM2:
```bash
pm2 status              # Jarayonlar statusini ko'rish
pm2 logs                # Logs ko'rish real-time
pm2 restart oquv-backend # Backend restart
pm2 stop oquv-backend   # To'xtatish
pm2 delete oquv-backend # O'chirish
pm2 monit               # Monitoring
```

### Nginx:
```bash
sudo systemctl status nginx
sudo systemctl restart nginx
sudo nginx -t                  # Config test
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

### System:
```bash
top                 # Jarayonlar monitori
df -h               # Disk joyi
free -h             # RAM holati
uptime              # Server uptime
```

---

## 💡 MUHIM MASLAHATLAR

### 1. Database Backup:
```bash
# Har kuni backup qilish uchun cron job
crontab -e

# Quyidagini qo'shing (har kuni soat 3 da):
0 3 * * * cp /home/opc/oquv-markazi/backend/oquv_markazi.db /home/opc/backups/oquv_backup_$(date +\%Y\%m\%d).db
```

### 2. SSL Sertifikat (Let's Encrypt):
```bash
sudo apt install certbot python3-certbot-nginx -y

# Domen bo'lsa:
sudo certbot --nginx -d sizning-domeningiz.com
```

### 3. Monitoring:
```bash
# htop o'rnatish
sudo apt install htop -y
htop
```

### 4. Logs tozalash:
```bash
# Eski loglarni tozalash
sudo journalctl --vacuum-time=7d
```

---

## ✅ CHECKLIST

Deploy jarayonida har bir qadamni belgilab boring:

- [ ] Oracle Cloud'da ro'yxatdan o'tdim
- [ ] SSH kalit yaratdim
- [ ] VM instance yaratdim (2 OCPU, 12GB RAM)
- [ ] Public IP oldim
- [ ] SSH orqali ulandim
- [ ] Node.js o'rnatdim
- [ ] PM2 o'rnatdim
- [ ] Nginx o'rnatdim
- [ ] Loyihani yukladim (Git/SCP)
- [ ] Backend sozladim (.env.production)
- [ ] Frontend sozladim (.env.production)
- [ ] Backend build qildim
- [ ] Frontend build qildim
- [ ] PM2 bilan ishga tushirdim
- [ ] Nginx konfiguratsiya qildim
- [ ] Oracle Cloud Firewall ochdim
- [ ] Server Firewall ochdim
- [ ] Sayt ochildi! ✅

---

## 🎉 TABRIKLAYMAN!

Sizning loyihangiz Oracle Cloud'da bepul deploy qilindi!

**Server manzili:** `http://<SERVER_IP>`

**Keyingi qadamlar:**
1. Domen sotib oling (ixtiyoriy)
2. SSL sertifikat o'rnating
3. Database backup avtomatlashtiring
4. Monitoring sozlang

---

## 🆘 YORDAM KERAKMI?

Agar muammo yuzaga kelsa:

1. **PM2 logs:** `pm2 logs`
2. **Nginx error logs:** `sudo tail -f /var/log/nginx/error.log`
3. **System logs:** `journalctl -xe`
4. **Oracle Cloud Console:** Instance metrics

**Barcha savollaringiz bo'yicha murojaat qiling!** 😊
