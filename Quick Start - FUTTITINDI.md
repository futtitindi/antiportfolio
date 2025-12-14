# Quick Start - FUTTITINDI

Inizia a usare FUTTITINDI in 5 minuti!

## 🚀 Avvio Rapido (Locale)

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

# Modifica .env.local con le tue credenziali
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

Visita http://localhost:3000 nel browser!

## 📝 Primo Portfolio

1. **Accedi** — Clicca "Accedi e Inizia"
2. **Compila il Form** — Rispondi alle 6 domande sulla tua impronta umana
3. **Genera** — Clicca "Genera il Mio Portfolio"
4. **Visualizza** — Vedi il tuo portfolio generato!

## 🔧 Configurazione Minima

Per far funzionare il progetto, hai bisogno di:

```env
DATABASE_URL=mysql://root:password@localhost:3306/futtitindi
JWT_SECRET=your_secret_key_here_min_32_chars
VITE_APP_ID=your_app_id
OAUTH_SERVER_URL=https://api.manus.im
BUILT_IN_FORGE_API_KEY=your_api_key
```

## 📚 Documentazione Completa

- **[INSTALLATION.md](./INSTALLATION.md)** — Guida di installazione dettagliata
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** — Come deployare in produzione
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** — Come contribuire al progetto
- **[README.md](./README.md)** — Documentazione completa

## 🆘 Problemi?

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

## 🎯 Prossimi Passi

1. **Personalizza il Form** — Modifica le domande in `client/src/pages/Home.tsx`
2. **Personalizza il Design** — Cambia i colori in `client/src/index.css`
3. **Aggiungi Feature** — Vedi [CONTRIBUTING.md](./CONTRIBUTING.md)
4. **Deploy** — Segui [DEPLOYMENT.md](./DEPLOYMENT.md)

## 🚀 Deploy Rapido su Manus

```bash
# 1. Connetti il repository a Manus
# 2. Configura le variabili d'ambiente
# 3. Clicca "Deploy"
```

Fatto! Il tuo portfolio è online! 🎉

---

Hai domande? Apri un [GitHub Issue](https://github.com/yourusername/futtitindi/issues)!
