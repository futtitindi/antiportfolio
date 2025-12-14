# Guida alla Contribuzione

Grazie per l'interesse nel contribuire a **FUTTITINDI - L'ANTI-PORTFOLIO**! Questo documento fornisce linee guida e istruzioni per contribuire al progetto.

## 📋 Codice di Condotta

Tutti i contributori devono seguire il nostro Codice di Condotta:

- Sii rispettoso verso gli altri
- Accetta critiche costruttive
- Focalizzati su ciò che è meglio per la comunità
- Mostra empatia verso gli altri membri della comunità

## 🚀 Come Iniziare

### 1. Fork il Repository

Clicca il pulsante "Fork" in alto a destra della pagina del repository.

### 2. Clone il tuo Fork

```bash
git clone https://github.com/YOUR_USERNAME/futtitindi.git
cd futtitindi
```

### 3. Aggiungi l'upstream Remote

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/futtitindi.git
```

### 4. Crea un Branch per la tua Feature

```bash
git checkout -b feature/your-feature-name
```

## 💻 Setup Locale

```bash
# Installa le dipendenze
pnpm install

# Configura le variabili d'ambiente
cp .env.example .env.local

# Esegui le migrazioni del database
pnpm db:push

# Avvia il dev server
pnpm dev
```

## ✍️ Processo di Contribuzione

### 1. Crea un Issue

Prima di iniziare a lavorare su una feature, crea un issue per discuterne:

- Descrivi il problema o la feature
- Spiega il tuo approccio proposto
- Attendi il feedback del team

### 2. Sviluppa la tua Feature

- Mantieni il codice pulito e leggibile
- Segui lo stile di codice del progetto
- Scrivi test per le nuove funzionalità
- Aggiorna la documentazione se necessario

### 3. Commit dei Tuoi Cambiamenti

Usa commit messages chiari e descrittivi:

```bash
git commit -m "feat: add portfolio export to PDF"
git commit -m "fix: resolve portfolio generation timeout"
git commit -m "docs: update README with new features"
```

**Formato dei Commit:**
- `feat:` per nuove feature
- `fix:` per bug fixes
- `docs:` per documentazione
- `style:` per cambiamenti di stile
- `refactor:` per refactoring del codice
- `test:` per test
- `chore:` per manutenzione

### 4. Push dei Cambiamenti

```bash
git push origin feature/your-feature-name
```

### 5. Apri una Pull Request

1. Vai al repository originale su GitHub
2. Clicca "New Pull Request"
3. Seleziona il tuo branch
4. Descrivi i tuoi cambiamenti in dettaglio
5. Clicca "Create Pull Request"

## 📝 Linee Guida per il Codice

### TypeScript

- Usa type annotations esplicite
- Evita `any` quando possibile
- Usa `interface` per oggetti, `type` per union types

```typescript
// ✅ Buono
interface Portfolio {
  id: string;
  title: string;
  content: PIUContent;
}

// ❌ Cattivo
const portfolio: any = { ... };
```

### React

- Usa functional components
- Usa hooks per state management
- Evita prop drilling, usa Context quando necessario
- Scrivi componenti riutilizzabili

```typescript
// ✅ Buono
export function PortfolioCard({ portfolio }: { portfolio: Portfolio }) {
  return <div>{portfolio.title}</div>;
}

// ❌ Cattivo
export function PortfolioCard(props) {
  return <div>{props.portfolio.title}</div>;
}
```

### CSS/Tailwind

- Usa Tailwind utilities al posto di CSS custom
- Mantieni le classi organizzate
- Evita inline styles

```jsx
// ✅ Buono
<div className="flex items-center justify-between p-4 bg-slate-900 rounded-lg">
  {/* content */}
</div>

// ❌ Cattivo
<div style={{ display: 'flex', justifyContent: 'space-between' }}>
  {/* content */}
</div>
```

### Naming Conventions

- **Components**: PascalCase (e.g., `PortfolioCard.tsx`)
- **Functions**: camelCase (e.g., `generatePortfolio()`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_PORTFOLIO_LENGTH`)
- **Files**: kebab-case o PascalCase per components

## 🧪 Testing

Scrivi test per le tue feature:

```bash
# Esegui i test
pnpm test

# Esegui i test in watch mode
pnpm test:watch

# Genera coverage report
pnpm test:coverage
```

**Esempio di test:**

```typescript
import { describe, it, expect } from 'vitest';
import { generatePortfolio } from './portfolio';

describe('Portfolio Generation', () => {
  it('should generate portfolio with valid input', async () => {
    const result = await generatePortfolio({
      title: 'Test Portfolio',
      description: 'Test',
    });
    
    expect(result).toBeDefined();
    expect(result.id).toBeDefined();
  });
});
```

## 📚 Documentazione

Quando aggiungi una nuova feature:

1. Aggiorna il README.md se necessario
2. Aggiungi commenti JSDoc per le funzioni pubbliche
3. Aggiorna il file CONTRIBUTING.md se le linee guida cambiano

```typescript
/**
 * Generates a portfolio based on user input
 * @param input - The user's professional information
 * @returns The generated portfolio
 */
export async function generatePortfolio(input: ProfessionalInput): Promise<Portfolio> {
  // implementation
}
```

## 🔍 Code Review

Tutti i PR devono essere revisionati prima di essere merged:

- Sii aperto ai feedback
- Rispondi alle domande del reviewer
- Apporta i cambiamenti richiesti
- Chiedi chiarimenti se necessario

## 🐛 Segnalazione di Bug

Se trovi un bug:

1. Controlla se è già stato segnalato in Issues
2. Se no, crea un nuovo issue con:
   - Descrizione chiara del bug
   - Passi per riprodurlo
   - Comportamento atteso vs attuale
   - Screenshot/video se applicabile
   - Versione del progetto e ambiente

## 🎯 Aree di Contribuzione

### Priorità Alta

- Bug fixes
- Miglioramenti di performance
- Documentazione
- Test coverage

### Priorità Media

- Nuove feature minori
- Miglioramenti UX
- Refactoring del codice

### Priorità Bassa

- Aggiornamenti di dipendenze
- Cleanup del codice
- Commenti e documentazione interna

## 📦 Rilascio di Nuove Versioni

Il team mantiene un changelog in `CHANGELOG.md`. Le versioni seguono [Semantic Versioning](https://semver.org/):

- MAJOR: breaking changes
- MINOR: nuove feature compatibili
- PATCH: bug fixes

## 🤝 Domande?

Se hai domande:

1. Controlla la documentazione
2. Apri un issue per discussione
3. Contatta il team di sviluppo

## 📄 Licenza

Contribuendo a questo progetto, accetti che i tuoi contributi siano licenziati sotto la MIT License.

---

Grazie per aver contribuito a FUTTITINDI! 🚀
