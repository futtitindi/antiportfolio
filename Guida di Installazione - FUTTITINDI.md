# Guida di Installazione - FUTTITINDI

Questa guida ti aiuterà a installare e configurare FUTTITINDI - L'ANTI-PORTFOLIO sul tuo sistema locale o su un server.

## 📋 Prerequisiti

Prima di iniziare, assicurati di avere installato:

- **Node.js 22.x o superiore** — [Download](https://nodejs.org/)
- **pnpm 10.x o superiore** — `npm install -g pnpm`
- **Git** — [Download](https://git-scm.com/)
- **MySQL 8.0+ o TiDB** — [Download](https://www.mysql.com/downloads/) o [TiDB Cloud](https://tidbcloud.com/)

### Verifica delle Versioni

```bash
node --version      # v22.x.x
pnpm --version      # 10.x.x
git --version       # 2.x.x
mysql --version     # 8.0.x
```

## 🚀 Installazione Locale

### Step 1: Clone il Repository

```bash
git clone https://github.com/yourusername/futtitindi.git
cd futtitindi
```

### Step 2: Installa le Dipendenze

```bash
pnpm install
```

Questo comando installerà tutte le dipendenze del progetto sia per il frontend che per il backend.

### Step 3: Configura il Database

#### Opzione A: MySQL Locale

1. **Crea il database:**

```bash
mysql -u root -p -e "CREATE DATABASE futtitindi CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
```

2. **Crea un utente (opzionale ma consigliato):**

```bash
mysql -u root -p -e "CREATE USER 'futtitindi'@'localhost' IDENTIFIED BY 'your_password'; GRANT ALL PRIVILEGES ON futtitindi.* TO 'futtitindi'@'localhost'; FLUSH PRIVILEGES;"
```

#### Opzione B: TiDB Cloud

1. Vai su [TiDB Cloud](https://tidbcloud.com/)
2. Crea un nuovo cluster
3. Copia la connection string

### Step 4: Configura le Variabili d'Ambiente

Crea un file `.env.local` nella root del progetto:

```bash
cp .env.example .env.local
```

Modifica `.env.local` con le tue credenziali:

```env
# Database
DATABASE_URL=mysql://username:password@localhost:3306/futtitindi

# OAuth (da Manus)
VITE_APP_ID=your_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://manus.im

# JWT Secret (genera una stringa casuale di 32+ caratteri)
JWT_SECRET=your_random_secret_key_here_min_32_chars

# LLM API (da Manus)
BUILT_IN_FORGE_API_URL=https://api.manus.im
BUILT_IN_FORGE_API_KEY=your_api_key
VITE_FRONTEND_FORGE_API_KEY=your_frontend_key
VITE_FRONTEND_FORGE_API_URL=https://api.manus.im

# Owner Info
OWNER_NAME=Your Name
OWNER_OPEN_ID=your_open_id
```

### Step 5: Esegui le Migrazioni del Database

```bash
pnpm db:push
```

Questo comando creerà tutte le tabelle necessarie nel database.

### Step 6: Avvia il Dev Server

```bash
pnpm dev
```

Il server sarà disponibile su:
- **Frontend**: http://localhost:5173
- **Backend**: http://localhost:3000

## 🌐 Installazione su Server (Production)

### Step 1: Prepara il Server

```bash
# Aggiorna il sistema
sudo apt update && sudo apt upgrade -y

# Installa Node.js
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs

# Installa pnpm
npm install -g pnpm

# Installa Git
sudo apt install -y git

# Installa MySQL (opzionale, se non usi TiDB Cloud)
sudo apt install -y mysql-server
```

### Step 2: Clone il Repository

```bash
cd /var/www
sudo git clone https://github.com/yourusername/futtitindi.git
cd futtitindi
sudo chown -R $USER:$USER .
```

### Step 3: Installa le Dipendenze

```bash
pnpm install --prod
```

### Step 4: Configura le Variabili d'Ambiente

```bash
nano .env.local
```

Aggiungi le configurazioni necessarie (vedi Step 4 della sezione locale).

### Step 5: Build il Progetto

```bash
pnpm build
```

### Step 6: Esegui le Migrazioni

```bash
pnpm db:push
```

### Step 7: Avvia il Server con PM2

```bash
# Installa PM2
npm install -g pm2

# Avvia l'applicazione
pm2 start "pnpm start" --name "futtitindi"

# Salva la configurazione PM2
pm2 save

# Abilita PM2 al boot
pm2 startup
```

### Step 8: Configura Nginx (Reverse Proxy)

```bash
sudo nano /etc/nginx/sites-available/futtitindi
```

Aggiungi questa configurazione:

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Abilita il sito:

```bash
sudo ln -s /etc/nginx/sites-available/futtitindi /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

### Step 9: Configura SSL con Let's Encrypt

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

## 🐳 Installazione con Docker

### Dockerfile

Crea un file `Dockerfile` nella root:

```dockerfile
FROM node:22-alpine

WORKDIR /app

# Installa pnpm
RUN npm install -g pnpm

# Copia package files
COPY pnpm-lock.yaml package.json ./

# Installa dipendenze
RUN pnpm install --frozen-lockfile

# Copia il codice
COPY . .

# Build
RUN pnpm build

# Esponi la porta
EXPOSE 3000

# Avvia l'app
CMD ["pnpm", "start"]
```

### docker-compose.yml

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=mysql://user:password@db:3306/futtitindi
      - VITE_APP_ID=${VITE_APP_ID}
      - OAUTH_SERVER_URL=${OAUTH_SERVER_URL}
      - JWT_SECRET=${JWT_SECRET}
      - BUILT_IN_FORGE_API_KEY=${BUILT_IN_FORGE_API_KEY}
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=futtitindi
      - MYSQL_USER=futtitindi
      - MYSQL_PASSWORD=password
    volumes:
      - db_data:/var/lib/mysql
    ports:
      - "3306:3306"

volumes:
  db_data:
```

Avvia con:

```bash
docker-compose up -d
```

## ✅ Verifica dell'Installazione

### Test del Database

```bash
pnpm db:push
```

Dovrebbe completarsi senza errori.

### Test del Server

```bash
pnpm dev
```

Visita http://localhost:3000 nel browser. Dovresti vedere la home page di FUTTITINDI.

### Test della Generazione Portfolio

1. Accedi con Manus OAuth
2. Compila il form
3. Clicca "Genera Portfolio"
4. Verifica che il portfolio sia generato correttamente

## 🔧 Troubleshooting

### Errore: "Cannot find module"

```bash
# Reinstalla le dipendenze
rm -rf node_modules pnpm-lock.yaml
pnpm install
```

### Errore: "Database connection failed"

1. Verifica che MySQL sia in esecuzione
2. Controlla le credenziali in `.env.local`
3. Verifica che il database esista

```bash
mysql -u root -p -e "SHOW DATABASES;"
```

### Errore: "Port 3000 already in use"

```bash
# Trova il processo che usa la porta
lsof -i :3000

# Termina il processo
kill -9 <PID>
```

### Errore: "OAuth not configured"

1. Verifica che `VITE_APP_ID` sia corretto
2. Controlla che `OAUTH_SERVER_URL` sia raggiungibile
3. Verifica le credenziali Manus

## 📚 Prossimi Passi

Dopo l'installazione:

1. Leggi la [Documentazione API](./API.md)
2. Consulta la [Guida di Sviluppo](./DEVELOPMENT.md)
3. Contribuisci al progetto — vedi [CONTRIBUTING.md](./CONTRIBUTING.md)

## 🆘 Supporto

Se hai problemi:

1. Controlla i [Common Issues](./TROUBLESHOOTING.md)
2. Apri un [GitHub Issue](https://github.com/yourusername/futtitindi/issues)
3. Contatta il team di supporto

---

Buona installazione! 🚀
