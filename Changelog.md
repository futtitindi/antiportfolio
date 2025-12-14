# Changelog

Tutti i cambiamenti notevoli di questo progetto saranno documentati in questo file.

Il formato è basato su [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
e questo progetto segue [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-14

### Added

- **Form Completamente Rivisitato** — Nuove domande incentrate su unicità umana e processo di pensiero
  - "Come vuoi essere ricordato?" — Impronta professionale unica
  - "Qual è il tuo processo di pensiero?" — Come affronti i problemi
  - "Quale problema risolvi meglio?" — La tua specialità
  - "Cosa ti rende insostituibile?" — Il tuo valore umano
  - "Quali lezioni dai tuoi fallimenti?" — La tua crescita
  - "Qual è la proof del tuo impatto?" — Risultati concreti

- **Modulo AI Aggiornato** — Generazione di portfolio focalizzata su impronta umana
  - Impronta Professionale Unica
  - Processo di Pensiero
  - Problema che Risolvi Meglio
  - Competenze Umane Distintive (5 skill)
  - Proof Tangibili di Impatto
  - Lezioni dai Fallimenti

- **PortfolioView Rinnovato** — Visualizzazione moderna del portfolio
  - Sezioni colorate e ben organizzate
  - Design responsive e accessibile
  - Rendering markdown per contenuti ricchi

- **Retry Handler con Exponential Backoff** — Gestione intelligente dei rate limit dell'API LLM
  - Retry automatico con backoff esponenziale
  - Jitter per evitare thundering herd
  - Logging dettagliato

- **Autenticazione Manus OAuth** — Integrazione completa
  - Login/logout
  - Session management
  - User context in tRPC procedures

- **Database MySQL/TiDB** — Schema completo
  - Tabella portfolios con slug unico
  - Metadati e timestamp
  - Contenuti generati salvati

- **tRPC API** — Procedure complete
  - `portfolio.create` — Creazione portfolio
  - `portfolio.generateContent` — Generazione AI
  - `portfolio.getBySlug` — Recupero pubblico
  - `portfolio.list` — Elenco utente

- **Documentazione Completa**
  - README.md con guida completa
  - INSTALLATION.md con setup locale e production
  - DEPLOYMENT.md con opzioni di hosting
  - CONTRIBUTING.md con linee guida
  - LICENSE MIT

### Changed

- Trasformazione completa da CV tradizionale a Portfolio di Impronta Umana
- Semplificazione del flusso di generazione (singola chiamata LLM)
- Miglioramento della gestione degli errori

### Fixed

- Risolto bug di rate limiting dell'API LLM
- Risolto problema di parsing JSON dai code blocks
- Risolto type mismatch tra array e stringhe nei dati

## [0.1.0] - 2025-12-13

### Initial Release

- Setup iniziale del progetto con template tRPC + Manus Auth + Database
- Struttura base del frontend e backend
- Configurazione del database schema
- Setup OAuth integration

---

## Versioning

- **MAJOR**: Breaking changes (es. cambio API, schema database)
- **MINOR**: Nuove feature compatibili (es. nuove sezioni portfolio)
- **PATCH**: Bug fixes (es. correzioni di rendering)

## Release Process

1. Aggiorna il CHANGELOG.md
2. Aggiorna il version number in package.json
3. Crea un git tag: `git tag v1.0.0`
4. Push il tag: `git push origin v1.0.0`
5. Crea una GitHub Release

## Roadmap Futuro

### v1.1.0 (Q1 2025)

- [ ] Export PDF del portfolio
- [ ] Export HTML statico
- [ ] Editor inline per modificare sezioni
- [ ] Galleria di portfolio di esempio
- [ ] Analytics per portfolio pubblici

### v1.2.0 (Q2 2025)

- [ ] Multi-language support (EN, FR, ES, DE)
- [ ] Dark/Light theme toggle
- [ ] Portfolio templates personalizzati
- [ ] Integrazione LinkedIn
- [ ] Integrazione GitHub

### v2.0.0 (Q3 2025)

- [ ] Collaborazione real-time
- [ ] Versioning e history portfolio
- [ ] Sistema di commenti
- [ ] Portfolio team
- [ ] API pubblica per integrazioni

---

Per domande su una versione specifica, apri un [GitHub Issue](https://github.com/yourusername/futtitindi/issues).
