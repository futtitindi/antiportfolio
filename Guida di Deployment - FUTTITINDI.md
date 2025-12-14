# Guida di Deployment - FUTTITINDI

Questa guida copre i diversi modi per deployare FUTTITINDI in produzione.

## 🎯 Opzioni di Deployment

1. **Manus Platform** (Consigliato) — Hosting integrato con OAuth e LLM
2. **Railway** — Deployment semplice con GitHub integration
3. **Render** — Hosting gratuito con database PostgreSQL
4. **Vercel** — Ottimo per il frontend, backend su serverless
5. **Self-Hosted** — Server proprio con Docker

## 🚀 Deployment su Manus Platform (Consigliato)

### Step 1: Connetti il Repository GitHub

1. Vai su [Manus Dashboard](https://manus.im/dashboard)
2. Clicca "New Project"
3. Seleziona "Connect GitHub Repository"
4. Autorizza Manus ad accedere ai tuoi repository
5. Seleziona il repository `futtitindi`

### Step 2: Configura le Variabili d'Ambiente

Nel dashboard Manus:

1. Vai a "Settings" → "Environment Variables"
2. Aggiungi le seguenti variabili:

```
DATABASE_URL=your_database_url
JWT_SECRET=your_jwt_secret
VITE_APP_ID=your_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://manus.im
BUILT_IN_FORGE_API_KEY=your_api_key
BUILT_IN_FORGE_API_URL=https://api.manus.im
VITE_FRONTEND_FORGE_API_KEY=your_frontend_key
VITE_FRONTEND_FORGE_API_URL=https://api.manus.im
OWNER_NAME=Your Name
OWNER_OPEN_ID=your_open_id
```

### Step 3: Deploy

1. Clicca "Deploy"
2. Seleziona il branch `main`
3. Clicca "Deploy Now"

Manus deployerà automaticamente il progetto e lo renderà disponibile su un URL pubblico.

### Step 4: Configura il Dominio Personalizzato

1. Nel dashboard, vai a "Settings" → "Domains"
2. Aggiungi il tuo dominio personalizzato
3. Configura i DNS record secondo le istruzioni

## 🚂 Deployment su Railway

### Step 1: Crea un Account Railway

Vai su [Railway.app](https://railway.app) e crea un account.

### Step 2: Connetti il Repository GitHub

1. Clicca "New Project"
2. Seleziona "Deploy from GitHub repo"
3. Autorizza Railway
4. Seleziona il repository `futtitindi`

### Step 3: Configura il Database

1. Nel progetto Railway, clicca "Add Service"
2. Seleziona "MySQL"
3. Railway creerà un database MySQL

### Step 4: Configura le Variabili d'Ambiente

1. Vai a "Variables"
2. Aggiungi tutte le variabili necessarie (vedi sopra)
3. Railway fornirà automaticamente `DATABASE_URL` dal servizio MySQL

### Step 5: Deploy

Railway deployerà automaticamente quando fai push a `main`.

## 🎨 Deployment su Render

### Step 1: Crea un Account Render

Vai su [Render.com](https://render.com) e crea un account.

### Step 2: Crea un Nuovo Servizio Web

1. Clicca "New +"
2. Seleziona "Web Service"
3. Connetti il tuo repository GitHub

### Step 3: Configura il Servizio

- **Name**: futtitindi
- **Environment**: Node
- **Build Command**: `pnpm install && pnpm build`
- **Start Command**: `pnpm start`

### Step 4: Aggiungi il Database

1. Clicca "New +"
2. Seleziona "PostgreSQL"
3. Render fornirà la connection string

### Step 5: Configura le Variabili d'Ambiente

Nella sezione "Environment", aggiungi tutte le variabili necessarie.

### Step 6: Deploy

Clicca "Create Web Service". Render deployerà automaticamente.

## ⚡ Deployment su Vercel (Frontend) + Backend Separato

### Step 1: Deploy il Frontend su Vercel

```bash
npm install -g vercel
vercel
```

Segui le istruzioni di Vercel.

### Step 2: Deploy il Backend su Railway/Render

Usa le istruzioni sopra per deployare il backend.

### Step 3: Configura le Variabili d'Ambiente del Frontend

Nel progetto Vercel, aggiungi:

```
VITE_FRONTEND_FORGE_API_URL=https://your-backend.com
VITE_FRONTEND_FORGE_API_KEY=your_key
```

## 🐳 Self-Hosted con Docker

### Step 1: Prepara il Server

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io docker-compose git
sudo usermod -aG docker $USER
```

### Step 2: Clone il Repository

```bash
git clone https://github.com/yourusername/futtitindi.git
cd futtitindi
```

### Step 3: Configura le Variabili d'Ambiente

```bash
nano .env.local
```

Aggiungi tutte le variabili necessarie.

### Step 4: Build e Avvia con Docker Compose

```bash
docker-compose up -d
```

### Step 5: Configura Nginx

```bash
sudo apt install -y nginx
```

Crea `/etc/nginx/sites-available/futtitindi`:

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

Abilita:

```bash
sudo ln -s /etc/nginx/sites-available/futtitindi /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

### Step 6: Configura SSL

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

## 📊 Monitoraggio Post-Deployment

### Manus Platform

1. Dashboard → "Analytics" per traffico e performance
2. "Logs" per errori e debug
3. "Metrics" per CPU, memoria, database

### Railway/Render

Entrambi forniscono dashboard di monitoraggio integrati.

### Self-Hosted

Usa PM2 per monitorare:

```bash
pm2 monit
pm2 logs futtitindi
```

## 🔄 CI/CD Pipeline

### GitHub Actions

Crea `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Install dependencies
        run: npm install -g pnpm && pnpm install
      
      - name: Run tests
        run: pnpm test
      
      - name: Build
        run: pnpm build
      
      - name: Deploy to Manus
        run: |
          # Aggiungi il tuo script di deployment
```

## 🚨 Troubleshooting Deployment

### Errore: "Database connection failed"

```bash
# Verifica la connection string
echo $DATABASE_URL

# Testa la connessione
mysql -h host -u user -p database
```

### Errore: "Out of memory"

Aumenta la memoria del container:

```yaml
# docker-compose.yml
services:
  app:
    mem_limit: 2g
```

### Errore: "Port already in use"

```bash
# Cambia la porta nel docker-compose.yml
ports:
  - "8080:3000"
```

### Errore: "Build failed"

1. Controlla i log di build
2. Verifica che tutte le dipendenze siano installate
3. Controlla la versione di Node.js

## 📈 Scaling

### Aumenta le Risorse

- **CPU**: Aumenta i core del container
- **Memoria**: Aumenta la RAM allocata
- **Database**: Scala il database MySQL

### Load Balancing

Per traffico alto, usa un load balancer:

```nginx
upstream backend {
    server app1:3000;
    server app2:3000;
    server app3:3000;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
    }
}
```

## 🔐 Sicurezza

### Checklist Pre-Deployment

- [ ] Tutte le variabili d'ambiente configurate
- [ ] Database con password forte
- [ ] SSL/TLS abilitato
- [ ] CORS configurato correttamente
- [ ] Rate limiting abilitato
- [ ] Logging e monitoring attivi
- [ ] Backup del database configurati

### Backup Automatici

```bash
# Backup giornaliero del database
0 2 * * * mysqldump -u user -p password database > /backups/db-$(date +\%Y\%m\%d).sql
```

## 📞 Supporto

Per problemi di deployment:

1. Controlla i log dell'applicazione
2. Verifica le variabili d'ambiente
3. Apri un issue su GitHub
4. Contatta il supporto della piattaforma di hosting

---

Buon deployment! 🚀
