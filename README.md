# Challenge BitBoss — Worker Gantt

Test di UX design per **BitBoss** (modulo dentro *DOT*).

**Deliverable unico:** [`worker-gantt.html`](./worker-gantt.html) — un solo file, HTML + CSS + JavaScript vanilla, **zero build, zero dipendenze**.

---

## Il problema

Dare al team, **a colpo d'occhio**, la fotografia dell'allocazione **futura** di ogni
worker. Il segnale dominante è la **capacità libera da vendere**: quante ore ogni
persona ha ancora disponibili, settimana per settimana.

## L'interfaccia

- **L1 — Overview:** una riga per worker con il Gantt delle prossime settimane;
  la capacità libera è l'elemento visivamente prioritario.
- **L2 — Dettaglio:** espandendo un worker si vede la ripartizione per progetto.
- **Settimana selezionata:** header + banda sulla colonna, con codifica ridondante
  (grassetto + barra d'accento + cornice + `aria-checked`) — mai solo colore.
- **Filtri:** ricerca per nome e "solo disponibili"; l'ordinamento porta in alto
  chi ha più ore libere nella settimana selezionata.

## Principi di design

- **Semplicità radicale** — niente cruscotti sovraccarichi, un solo messaggio per vista.
- **WCAG 2.1 AA** — contrasto ≥ 4.5:1, navigazione da tastiera completa
  (radiogroup della settimana con frecce / Home / End / Enter / Space, roving tabindex),
  `prefers-reduced-motion` rispettato.
- **Codifica ridondante** — l'informazione non è mai affidata al solo colore.

## Come eseguirlo

Nessuna installazione. Basta aprire il file nel browser:

```bash
open worker-gantt.html
```

Oppure servirlo in locale (utile per ricaricare senza cache):

```bash
python3 -m http.server 8777
# poi apri http://localhost:8777/worker-gantt.html
```

## Perché vanilla (e non un framework)

L'app è una singola vista interattiva con dati statici di demo. Un framework
aggiungerebbe toolchain, bundle e superficie di manutenzione senza alcun beneficio.
Il file è auto-contenuto, ispezionabile e portabile ovunque: la scelta più pulita
per questo scope.

## Struttura del codice

Tutto in `worker-gantt.html`, con lo `<script>` organizzato in sezioni commentate:
dati → date/format → stato cella (`cellState`, singola fonte di verità) → render →
selezione settimana → filtri/ordinamento → interazioni (tooltip, sticky header) → init.
