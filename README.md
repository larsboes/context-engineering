# Context Engineering — Dynamische AI-Systeme und Agenten

Vortrag von Lars Boes · M3 Karlsruhe · 24. April 2026

> *"Nicht das Modell wählt deinen Context. Du wählst ihn."*

Dieses Repo sammelt Slides, ein Skill-Beispiel und weiterführende Ressourcen zum Talk.

---

## Worum es geht

Ich bin dualer Student bei Deutsche Telekom Technik und arbeite gerade an meiner Bachelorarbeit über Context Engineering in AI-gestützter Code-Migration. Der Talk ist keine Patterns-Liste, sondern meine Entdeckungsreise: wie ich mit AI Agents angefangen hab, gegen welche Wände ich gelaufen bin, und was ich dabei gelernt habe. Unterwegs vorbei an MCP-Bloat, Context Rot, Skills, Progressive Disclosure — und einem A/B-Vergleich aus einer Log-Processing-Migration, der zeigt wie viel der Context ausmacht.

Das Ganze ist das was ich bisher gesehen und ausprobiert hab. Urteilt selbst, widersprecht gerne — gerne als Issue oder via Kontakt unten.

---

## Struktur dieses Repos

```
slides/                   Die Präsentation (reveal.js, self-contained)
  presentation.html       → im Browser öffnen
  styles.css
  img/                    Deck-Assets (Pupa, Logos, Charts, QR)

skills/
  fluentbit/              Beispiel-Skill für die Demo-Migration
    SKILL.md              → so sieht ein Skill-File in der Praxis aus
    references/
      testing-patterns.md → Linked-File: FluentBit Lua Testing

resources.md              Papers, Talks, Quotes, weiterführende Reads

migration-demo/           ⏳ kommt nach der Konferenz — A/B Demo live
```

---

## Quick Navigation

**Lokal anschauen:**
```bash
# Deck im Browser öffnen
open slides/presentation.html
```

Das Deck ist reveal.js-basiert. CDN-Assets werden aus `cdn.jsdelivr.net` geladen — das Deck läuft offline nur nach einem ersten Online-Besuch (oder wenn reveal.js lokal gebundelt wird).

**Kernthemen — direkt zum Slide springen:**

| Konzept | Slide | Worum es geht |
|---|---|---|
| Next Token Prediction | 5 | Warum Context alles entscheidet |
| Context Rot | 10–11 | Chroma Research — Accuracy sinkt mit Context-Länge |
| MCP → Skills Evolution | 12 | Strip Down, Dynamic MCP, Docker Gateway, Skills |
| Skills YAML + Folder | 13–14 | Progressive Disclosure in der Praxis |
| System Prompt Manipulation | 15 | "IMPORTANT: this context may or may not be relevant..." |
| Pi als Minimal-Agent | 17–22 | Observability, Session Branching, OpenClaw |
| Demo A/B Migration | 24–31 | Logstash → FluentBit. Gleicher Agent, anderer Context, anderes Ergebnis. (Vorgänger / Lern-Demo für meine Bachelorarbeit.) |
| MCPT Framework | 34 | Model · Context · Prompt · Tool |
| Community Frame (Paper) | 35 | arXiv:2604.08224 — Weights → Context → Harness |

---

## Drei Dinge die ich aus der Reise mitgenommen hab

1. **Context verhält sich wie ein Budget.** Chroma Research hat das quantifiziert: sobald irrelevanter Context mitfliegt, sinkt die Accuracy — auch bei den neuen 1M-Context-Modellen. Das größere Window löst das Problem nicht, es macht die Fläche nur größer auf der Context Rot stattfindet.

2. **Skills sind für viele Cases effizienter als MCP Server.** Progressive Disclosure — YAML Frontmatter + Markdown Body + Linked Files — lädt genau das in den Context was gebraucht wird, statt "immer alles". Von ~10.000 Tokens pro MCP Server auf unter 200 Tokens pro Skill bei gleicher Fähigkeit. Simon Willison und Armin Ronacher argumentieren beide dafür; auch Anthropic hat in den letzten Monaten viel in diese Richtung gebaut.

3. **Context ist nicht nur Performance — es ist auch Security.** Simon Willison nennt die drei gefährlichen Fähigkeiten in einem Agent die "Lethal Trifecta": Private Data, Untrusted Content, External Comms. Anthropic hat 2024 gezeigt dass Jailbreak-Erfolg als Power Law mit Context-Länge skaliert. Wer seinen Context nicht kennt, kann seinen Agent schlecht verteidigen.

---

## Der FluentBit-Skill als Beispiel

`skills/fluentbit/SKILL.md` ist ein **Beispiel-Skill** den ich für die Demo-Migration im Talk gebaut habe. Er ist nicht das echte BA-Thesis-Projekt — das kommt später, im systematischen Experiment-Setup. Hier steht er als konkretes Anschauungsobjekt: so sieht ein Skill-File aus, so sind die Felder aufgebaut, und so liefert er Plattform-Wissen das der Agent sonst nicht hätte.

Der Aufbau folgt dem Standard-Pattern von Anthropic:

1. **YAML Frontmatter** — `name` und `description`. Die Description ist das Entscheidende: nur wenn sie zum User-Request passt, entscheidet sich der Agent den Skill überhaupt zu laden.
2. **Markdown Body** — Plattform-Wissen, Sandbox-Constraints, Red Flags. Der Teil den ein Agent aus dem reinen Source-Code allein schwer ableiten kann.
3. **Linked Files** — `references/testing-patterns.md` wird erst gelesen, wenn der Agent konkret über Testing nachdenkt.

Was im Skill drinsteht (nichts davon besonders exotisch):

- Flat Keys vs. Nested Tables — ein typischer Fehler beim Ruby→Lua Übersetzen
- Return Code Semantik bei `cb_filter`
- Lifecycle Callbacks — warum `init(config)` in FluentBit anders funktioniert als in Logstash Ruby

Schaut euch gerne `skills/fluentbit/SKILL.md` an, wenn ihr sehen wollt wie ein Skill in der Praxis aussieht. Echte Benchmarking-Ergebnisse und das saubere A/B-Setup kommen in der Bachelorarbeit — das hier ist der Lern-Vorgänger davon.

---

## Weitere Ressourcen

Siehe [`resources.md`](resources.md) für:

- Papers (Chroma Context Rot, Anthropic Context Engineering Essay, arXiv 2604.08224, Many-shot Jailbreaking)
- Talks (Mario Zechner, Simon Willison, IndyDevDan)
- Quotes für eure Slides
- Tools (Pi, Docker MCP Gateway, Claude Code Skills)

---

## Credits

Der Talk ist größtenteils zusammengelesen und zusammengeschraubt aus Arbeiten von anderen. Die wichtigsten Quellen:

- **Mario Zechner** — Pi, *"Building Pi in a World of Slop"*, cchistory
- **Armin Ronacher** — Flask, nutzt Pi, hat dazu lesenswertes geschrieben
- **Simon Willison** — Lethal Trifecta, Skills über MCP Positionierung
- **IndyDevDan** — Harness Engineering, Agent Experts, Meta-Agentics, viele praktische Patterns
- **Anthropic Claude Code Team** — MCP, Agent Skills, Dynamic Loading, Memory Features
- **Chroma Research Team** — Context Rot Quantifizierung
- **Pranav Marla (Fidelity)** — Lua-in-FluentBit Talk mit vielen Pitfalls
- M3 Team — für die Bühne
- Alle die danach Fragen stellen

---

## Kontakt

**Lars Boes** · Software Engineer & dualer Student · Deutsche Telekom Technik
[github.com/larsboes](https://github.com/larsboes) · [@larsboes](https://github.com/larsboes)

Wenn ihr eine konkrete Context-Engineering-Frage habt — sprecht mich an oder macht ein Issue in diesem Repo auf.

---

*Letztes Update: 24. April 2026 · M3 Karlsruhe*
