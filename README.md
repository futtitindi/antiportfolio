# FUTTITINDI - L'ANTI-PORTFOLIO 🎯

[![GitHub Release](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com/yourusername/futtitindi/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D22.0.0-brightgreen)](https://nodejs.org/)
[![pnpm Version](https://img.shields.io/badge/pnpm-%3E%3D10.0.0-brightgreen)](https://pnpm.io/)

**Un tool AI-powered che genera portfolio professionali valorizzando l'unicità umana, il processo di pensiero e la metodologia personale — non i job titles tradizionali.**

## 🎯 Cosa è FUTTITINDI?

FUTTITINDI rifiuta il formato CV tradizionale. Invece di chiedere "Qual è il tuo titolo?", chiede domande che rivelano la tua vera essenza professionale:

- **Come vuoi essere ricordato?** — La tua impronta unica
- **Qual è il tuo processo di pensiero?** — Come affronti i problemi
- **Quale problema risolvi meglio?** — La tua specialità
- **Cosa ti rende insostituibile?** — Il tuo valore umano
- **Quali lezioni dai tuoi fallimenti?** — La tua crescita
- **Qual è la proof del tuo impatto?** — Risultati concreti

Il risultato? Un portfolio che mostra **come pensi**, non solo **cosa hai fatto**.

## ✨ Caratteristiche Principali

| Caratteristica | Descrizione |
|---|---|
| 🎯 **Zero Job Titles** | Valorizza l'unicità, non il titolo |
| 🧠 **Processo su Output** | Mostra come pensi, non solo cosa hai fatto |
| 🤖 **AI-Powered** | Generazione intelligente di contenuti personalizzati |
| 🔐 **Autenticazione OAuth** | Login sicuro con Manus |
| 📱 **Design Responsive** | Funziona su desktop, tablet, mobile |
| 💾 **Database Integrato** | Salva e condividi i tuoi portfolio |
| 🚀 **Deployment Ready** | Pronto per production su Manus, Railway, Render |

## 🚀 Quick Start (5 Minuti)

### 1. Clone e Installa

```bash
git clone https://github.com/yourusername/futtitindi.git
cd futtitindi
pnpm install
```

### 2. Configura il Database

```bash
# Crea il database MySQL
mysql -u root -p -e "CREATE DATABASE futtitindi;"

# Copia il file di configurazione
cp .env.example .env.local

# Modifica con le tue credenziali (vedi sezione Setup)
nano .env.local
```

### 3. Esegui le Migrazioni

```bash
pnpm db:push
```

### 4. Avvia il Server

```bash
pnpm dev
```

Visita **http://localhost:3000** nel browser!

## 🔧 Configurazione Minima

Crea un file `.env.local` nella root del progetto con queste variabili:

```env
# Database
DATABASE_URL=mysql://root:password@localhost:3306/futtitindi

# JWT Secret (genera una stringa casuale di 32+ caratteri)
JWT_SECRET=your_random_secret_key_here_min_32_chars

# Manus OAuth
VITE_APP_ID=your_manus_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://manus.im

# LLM API (per generazione contenuti)
BUILT_IN_FORGE_API_URL=https://api.manus.im
BUILT_IN_FORGE_API_KEY=your_api_key
VITE_FRONTEND_FORGE_API_KEY=your_frontend_key
VITE_FRONTEND_FORGE_API_URL=https://api.manus.im

# Owner Info
OWNER_NAME=Your Name
OWNER_OPEN_ID=your_open_id
```

## 📋 Prerequisiti

Prima di iniziare, assicurati di avere:

- **Node.js 22.x o superiore** — [Download](https://nodejs.org/)
- **pnpm 10.x o superiore** — `npm install -g pnpm`
- **Git** — [Download](https://git-scm.com/)
- **MySQL 8.0+ o TiDB** — [Download](https://www.mysql.com/downloads/)

Verifica le versioni:

```bash
node --version      # v22.x.x
pnpm --version      # 10.x.x
git --version       # 2.x.x
mysql --version     # 8.0.x
```

## 📝 Primo Portfolio

1. **Accedi** — Clicca "Accedi e Inizia"
2. **Compila il Form** — Rispondi alle 6 domande sulla tua impronta umana
3. **Genera** — Clicca "Genera il Mio Portfolio"
4. **Visualizza** — Vedi il tuo portfolio generato!

## 🛠️ Stack Tecnologico

| Layer | Tecnologia |
|-------|-----------|
| **Frontend** | React 19 + Tailwind CSS 4 + TypeScript |
| **Backend** | Express 4 + tRPC 11 + Node.js |
| **Database** | MySQL/TiDB + Drizzle ORM |
| **Auth** | Manus OAuth |
| **AI** | LLM API (Claude/OpenAI) |
| **Deployment** | Manus Platform, Railway, Render, Docker |

## 📁 Struttura del Progetto

```
futtitindi/
├── client/                    # Frontend React
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.tsx      # Form per generare portfolio
│   │   │   └── PortfolioView.tsx  # Visualizzazione portfolio
│   │   ├── components/       # Componenti UI
│   │   ├── lib/              # Utilities (tRPC client, etc)
│   │   ├── App.tsx           # Routes
│   │   └── main.tsx          # Entry point
│   └── public/               # Static assets
├── server/                    # Backend Express + tRPC
│   ├── ai.ts                 # AI content generation
│   ├── db.ts                 # Database queries
│   ├── routers/
│   │   └── portfolio.ts      # Portfolio tRPC procedures
│   └── _core/                # Framework internals
├── drizzle/                   # Database schema
│   └── schema.ts             # Table definitions
├── README.md                 # Questo file
├── QUICK_START.md            # Avvio rapido
├── INSTALLATION.md           # Guida di installazione
├── DEPLOYMENT.md             # Guida di deployment
├── CONTRIBUTING.md           # Linee guida di contribuzione
└── LICENSE                   # Licenza MIT
```

## 🔄 Flusso di Generazione Portfolio

```
1. Utente compila il form
        ↓
2. Form inviato al backend via tRPC
        ↓
3. AI analizza i dati
        ↓
4. Portfolio generato con 6 sezioni
        ↓
5. Portfolio salvato nel database
        ↓
6. Portfolio visualizzato all'utente
        ↓
7. Portfolio condivisibile via link pubblico
```

## 📚 Documentazione Completa

| Documento | Descrizione |
|-----------|-------------|
| **[QUICK_START.md](./QUICK_START.md)** | Avvio rapido in 5 minuti |
| **[INSTALLATION.md](./INSTALLATION.md)** | Guida di installazione dettagliata |
| **[DEPLOYMENT.md](./DEPLOYMENT.md)** | Come deployare in produzione |
| **[CONTRIBUTING.md](./CONTRIBUTING.md)** | Come contribuire al progetto |
| **[CHANGELOG.md](./CHANGELOG.md)** | Cronologia versioni e roadmap |
| **[GITHUB_SETUP.md](./GITHUB_SETUP.md)** | Setup del repository GitHub |
| **[GITHUB_UPLOAD.md](./GITHUB_UPLOAD.md)** | Come caricare su GitHub |

## 🚀 Deployment

### Opzione 1: Manus Platform (Consigliato)

```bash
# 1. Connetti il repository a Manus
# 2. Configura le variabili d'ambiente nel dashboard
# 3. Deploy automatico su push a main
```

### Opzione 2: Railway

1. Vai su [Railway.app](https://railway.app)
2. Connetti il repository GitHub
3. Railway creerà il database MySQL automaticamente
4. Deploy automatico

### Opzione 3: Docker

```bash
docker-compose up -d
```

Vedi [DEPLOYMENT.md](./DEPLOYMENT.md) per tutte le opzioni.

## 🐛 Troubleshooting

### "Port 3000 already in use"

```bash
lsof -i :3000
kill -9 <PID>
```

### "Database connection failed"

Verifica che MySQL sia in esecuzione:

```bash
mysql -u root -p -e "SELECT 1;"
```

### "Module not found"

```bash
rm -rf node_modules pnpm-lock.yaml
pnpm install
```

Vedi [INSTALLATION.md](./INSTALLATION.md) per altri problemi.

## 🧪 Testing

```bash
# Esegui i test
pnpm test

# Test in watch mode
pnpm test:watch

# Coverage report
pnpm test:coverage
```

## 📊 Sezioni del Portfolio Generato

Ogni portfolio include 6 sezioni generate dall'AI:

### 1. Impronta Professionale Unica
La tua essenza professionale e il tuo valore unico.

### 2. Processo di Pensiero
Come affronti i problemi e la tua metodologia di lavoro.

### 3. Problema che Risolvi Meglio
La tua specialità e perché sei la persona giusta.

### 4. Competenze Umane Distintive
5 skill umane che ti rendono insostituibile.

### 5. Proof Tangibili di Impatto
Risultati concreti con numeri e feedback.

### 6. Lezioni dai Fallimenti
Come i tuoi fallimenti ti hanno reso più forte.

## 🤝 Contribuire

Vogliamo il tuo aiuto! Vedi [CONTRIBUTING.md](./CONTRIBUTING.md) per:

- Come segnalare bug
- Come proporre nuove feature
- Come contribuire con codice
- Linee guida di stile

### Aree di Contribuzione

- 🐛 **Bug fixes** — Aiuta a risolvere i problemi
- ✨ **Nuove feature** — Aggiungi funzionalità
- 📚 **Documentazione** — Migliora le guide
- 🧪 **Test** — Aumenta la coverage

## 📈 Roadmap

### v1.1.0 (Q1 2025)

- [ ] Export PDF del portfolio
- [ ] Export HTML statico
- [ ] Editor inline per modificare sezioni
- [ ] Galleria di portfolio di esempio

### v1.2.0 (Q2 2025)

- [ ] Multi-language support
- [ ] Dark/Light theme toggle
- [ ] Portfolio templates personalizzati
- [ ] Integrazione LinkedIn

### v2.0.0 (Q3 2025)

- [ ] Collaborazione real-time
- [ ] Versioning e history
- [ ] Sistema di commenti
- [ ] API pubblica

## 📞 Supporto

Hai domande o problemi?

1. **Controlla la documentazione** — [INSTALLATION.md](./INSTALLATION.md), [DEPLOYMENT.md](./DEPLOYMENT.md)
2. **Apri un GitHub Issue** — [Issues](https://github.com/yourusername/futtitindi/issues)
3. **Partecipa alle Discussions** — [Discussions](https://github.com/yourusername/futtitindi/discussions)

## 📄 Licenza

Questo progetto è licenziato sotto la **MIT License** — vedi [LICENSE](./LICENSE) per i dettagli.

## 🙏 Ringraziamenti

Grazie a tutti i contributori e agli utenti di FUTTITINDI!

## 🚀 Inizia Subito

```bash
# 1. Clone
git clone https://github.com/yourusername/futtitindi.git
cd futtitindi

# 2. Installa
pnpm install

# 3. Configura
cp .env.example .env.local
# Modifica .env.local con le tue credenziali

# 4. Esegui migrazioni
pnpm db:push

# 5. Avvia
pnpm dev

# 6. Apri http://localhost:3000
```

---

**Fatto con ❤️ da FUTTITINDI Team**

Trasforma il tuo portfolio. Racconta la tua impronta umana. 🎯

[⭐ Metti una stella su GitHub](https://github.com/yourusername/futtitindi) se ti piace il progetto!
