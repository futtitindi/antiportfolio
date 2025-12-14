    ├── portfolios — Dati portfolio
    ├── portfolioSections — Sezioni PIU
    └── fileUploads — Metadati file
```

## Installazione e Setup

### Prerequisiti
- Node.js 22.x
- pnpm 10.x
- MySQL/TiDB database
- Manus OAuth credentials

### Passaggi di Installazione

1. **Clone il repository**
   ```bash
   git clone <repository-url>
   cd portfolio-generator-tool
   ```

2. **Installa dipendenze**
   ```bash
   pnpm install
   ```

3. **Configura le variabili di ambiente**
   
   Le seguenti variabili sono automaticamente iniettate dal sistema Manus:
   - `DATABASE_URL` — Stringa di connessione MySQL
   - `JWT_SECRET` — Secret per sessioni
   - `VITE_APP_ID` — OAuth app ID
   - `OAUTH_SERVER_URL` — OAuth server URL
   - `BUILT_IN_FORGE_API_KEY` — API key per LLM
   - `BUILT_IN_FORGE_API_URL` — API URL per LLM

4. **Esegui le migrazioni del database**
   ```bash
   pnpm db:push
   ```

5. **Avvia il server di sviluppo**
   ```bash
   pnpm dev
   ```

   Il server sarà disponibile su `http://localhost:3000`

## Utilizzo

### Creazione di un Portfolio

1. **Accedi** con Manus OAuth
2. **Compila il form** con:
   - Titolo portfolio
   - CV/Background professionale
   - Filosofia lavorativa
   - Interessi e passioni
   - Fallimenti e lezioni apprese
3. **Clicca "Genera Portfolio"** — L'AI analizza i dati e genera il portfolio PIU
4. **Visualizza il portfolio** — Layout unico e contenuti personalizzati
5. **Pubblica e condividi** — URL pubblico per condividere il portfolio

### Generazione Contenuti AI

Il tool utilizza LLM per:

1. **Analisi Profonda** — Estrae pattern unici dai dati forniti
2. **Identificazione Impronta** — Scopre la proposta di valore unica
3. **Generazione Narrativa** — Crea contenuti per le 5 sezioni PIU