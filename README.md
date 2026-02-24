# Tundr × Sanremo 2026

Sito live della guida alle serate del Festival di Sanremo 2026, curato da Tundr.

🌐 **Live:** https://sanremo2026.tundr.io (o simile, configurare su Netlify)

---

## Struttura del progetto

```
tundr-sanremo/
├── index.html           # App principale (single-page)
├── favicon.svg          # Logo Tundr lightning bolt
├── data/
│   ├── night1.js        # Scaletta Serata 1 – Martedì 24 feb
│   ├── night2.js        # Scaletta Serata 2 – Mercoledì 25 feb
│   ├── night3.js        # Scaletta Serata 3 – Giovedì 26 feb
│   ├── night4.js        # Scaletta Serata 4 – Venerdì 27 feb
│   └── night5.js        # Scaletta Serata 5 – Sabato 28 feb (Finale)
├── nights/              # PDF delle serate (archivio)
└── README.md
```

---

## Come aggiornare la scaletta di una serata

### 1. Metodo diretto (GitHub web)

1. Vai su `data/night2.js` (o night3, night4, night5)
2. Clicca **Edit** (matita in alto a destra)
3. Incolla la scaletta nel formato:

```js
window.NIGHTS_DATA[2] = {
  number: 2,
  date: "2026-02-25",
  label: "Mercoledì 25 febbraio",
  startHour: 20, startMin: 40,
  endHour: 1, endMin: 30,
  highlights: ["Ospite principale", "Momento speciale"],
  schedule: [
    {t:[20,40], a:"Apertura", s:"", d:"Descrizione breve", tp:"special"},
    {t:[20,55], a:"ARTISTA", s:"Titolo canzone", d:"Note extra", tp:"cat"},
    // ... altri item
  ]
};
```

4. **Commit** → il sito si aggiorna automaticamente via Netlify in ~30 secondi

### 2. Upload PDF serata

Carica il PDF in `nights/serata-N.pdf` — apparirà nel link archivio.

---

## Tipi di item (`tp`)

| Valore    | Badge             | Uso                          |
|-----------|-------------------|------------------------------|
| `watch`   | Da guardare 🟡    | Artisti/momenti consigliati  |
| `special` | Imperdibile ✦ 🟡  | Ospiti grandi, momenti wow   |
| `ospite`  | Ospite 🟠         | Ospite non in gara           |
| `cat`     | In gara 🔵        | Artisti in gara              |
| `skip`    | Puoi saltare ⚪   | Cambi abito, regie, etc.     |
| `pub`     | Pubblicità ⚫     | Pause pubblicitarie          |

---

## Aggiornare la classifica

Apri `index.html`, trova il blocco `const RANKING = [` e aggiorna i dati:

```js
const RANKING = [
  {pos:1, artist:"NOME", song:"Canzone", pts:"1234"},
  // ...
];
```

Fonte ufficiale aggiornata ogni sera: https://www.canzoniweb.com/sanremo-2026-classifica-finale-risultati-e-vincitore/

---

## Setup iniziale: GitHub + Netlify

### GitHub

1. Crea repo: `github.com/TundrDesign/sanremo-2026`
2. Carica tutti i file (drag & drop nella UI GitHub o `git push`)

### Netlify

1. Vai su [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
2. Seleziona GitHub → repo `TundrDesign/sanremo-2026`
3. Build settings:
   - **Publish directory:** `.` (root)
   - **Build command:** (lasciare vuoto — è HTML statico)
4. **Deploy site** → ottieni URL tipo `tundr-sanremo-2026.netlify.app`

### Dominio custom (es. sanremo.tundr.io)

1. In Netlify → **Domain settings** → **Add custom domain**
2. Aggiungi `sanremo2026.tundr.io` (o il dominio che preferisci)
3. Nel pannello DNS del tuo provider aggiungi:
   - `CNAME sanremo2026 → [your-netlify-app].netlify.app`
4. Netlify provvede automaticamente il certificato SSL ✅

### Auto-deploy

Ogni `git push` su `main` triggera un redeploy automatico in ~30 secondi.

---

## Workflow serale consigliato

```
Ore 19:00 → Ricevi PDF scaletta serata
     ↓
Chiedi a Claude di convertire il PDF in formato JS
     ↓
Copia il JS in data/nightN.js su GitHub
     ↓
Commit → Netlify aggiorna il sito in 30 secondi
     ↓
A fine serata: aggiorna classifica in index.html
```

---

## Invio PDF a Claude

Quando hai il PDF della serata successiva:
1. Caricalo su GitHub in `nights/serata-N.pdf`
2. Incollami il link o allega il PDF direttamente in chat
3. Genero il JS pronto da copiare in `data/nightN.js`

---

*Fatto con ❤️ da Tundr — il welfare che ti fa stare bene anche stasera*
