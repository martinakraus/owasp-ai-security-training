# 🎯 Level 6 & 7 — Eskalationsstrategie

> ⚠️ **Transparenz-Hinweis:** Für diese Level gibt es aktuell keine verlässliche, öffentlich nachvollziehbare Musterlösung — die Informationslage ist dünn, und Lakera passt die Challenges gelegentlich an. Statt einer erfundenen "Lösung" bekommt ihr hier einen **Techniken-Baukasten**, den ihr systematisch ausprobieren könnt. Testet selbst, bevor ihr etwas als Musterlösung weitergebt.

## Baukasten fortgeschrittener Techniken

| Technik                            | Neuer Begriff       | Grundidee                                                                                                                                                                                                              |
| ---------------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Encoding**                       | _Encoding-Bypass_   | Teile der Anweisung in Base64 oder einer anderen Kodierung verstecken, damit ein textbasierter Filter das Schlüsselwort nicht direkt erkennt. Das Zielmodell dekodiert es selbst und führt die Anweisung trotzdem aus. |
| **Reasoning-Hijacking**            | _Chain-of-Thought_  | Manche Modelle "denken laut" in einem sichtbaren oder internen Zwischenschritt. Scheinbare "Denk-Notizen" im Payload können die Priorität in diesem Schritt beeinflussen.                                              |
| **Mehrstufige Injection**          | _Staged Injection_  | Die Anweisung wird über zwei getrennte, für sich harmlos wirkende Einträge aufgebaut, die sich erst in Kombination entfalten.                                                                                          |
| **Autoritäts-Framing**             | _Authority Framing_ | Der Payload gibt sich als Systemmeldung oder Entwickler-Notiz aus ("\[SYSTEM-MAINTENANCE]"), um mehr Gewicht zu bekommen als eine gewöhnliche Nutzer-Notiz.                                                            |
| **Feedback-getriebenes Iterieren** | —                   | Die Fehler- bzw. Score-Rückmeldung gibt oft Hinweise, _warum_ ein Payload abgelehnt wurde — gezielt auswerten statt blind raten.                                                                                       |

## 📚 Gesamtüberblick: Level 1–7

| Level | Kern-Technik                                                       |
| ----- | ------------------------------------------------------------------ |
| 1     | Direkte, einfache Injection                                        |
| 2     | Bestehende Einträge überschreiben, Rückfragen unterbinden          |
| 3     | Vollständigkeits-Overwrite bei mehreren Einträgen                  |
| 4     | Anweisung als Datenformat tarnen (Guardrail-Umgehung)              |
| 5     | Formatierung glätten, Balance zwischen Tarnung & Unauffälligkeit   |
| 6–7   | Encoding, Reasoning-Hijacking, Staged Injection, Authority Framing |

Dieser Verlauf spiegelt gut wider, wie sich reale KI-Verteidigungen entwickeln: von "gar kein Schutz" über "einfache Regelfilter" bis zu "ein zweites Modell prüft die Eingabe" — und wie Angreifer:innen jede Stufe kontern. Genau dieser Wettlauf ist der Kern von **LLM01 (Prompt Injection)**, **LLM03 (Excessive Agency)** und **LLM08 (Hidden Context Exposure)** aus der [Bedrohungsübersicht](bedrohungsubersicht-owasp-top-10-fur-llm-anwendungen-2026.md).

## 🛡️ Schwachstelle & Behebung (Gesamtfazit MindfulChat)

**Ausgenutzte Schwachstelle über alle Level:** [LLM08:2026 — Hidden Context Exposure](https://genai.owasp.org/llm-top-10/), verstärkt durch fehlende Herkunftsprüfung von Memory-Daten.

**Das eigentliche Problem, zusammengefasst:** Je härter die Verteidigung (Level 1 → 7), desto ausgefeilter musste der Angriff werden — aber **keine** der Schutzschichten hat die Grundschwachstelle wirklich behoben, sie hat sie nur schwerer ausnutzbar gemacht. Das ist ein zentrales Muster in der KI-Sicherheit: Oberflächliche Abwehrmaßnahmen (Guardrails, Formatierungs-Checks) können umgangen werden, solange die strukturelle Ursache — keine Trennung von Daten und Anweisungen — bestehen bleibt.

**Wie behebt man das (theoretisch) — strukturell, nicht nur oberflächlich?**

* **Herkunftsprüfung (Provenance) auf Systemebene**, nicht nur auf Prompt-Ebene — z. B. digitale Signaturen für Memory-Einträge, die belegen, wer sie wann geschrieben hat.
* **Architektonische Trennung von Daten und Instruktionen**, wo technisch möglich (z. B. strukturierte Felder statt freiem Fließtext für Memory).
* **Least Privilege:** Ein Memory-Schreibzugriff sollte nicht automatisch Einfluss auf _alle_ zukünftigen Nutzer:innen haben.
* **Mehrschichtige Verteidigung**, aber mit dem Wissen, dass jede einzelne Schicht umgehbar sein kann — daher Monitoring und Mensch-in-der-Schleife für kritische Änderungen ergänzen.

> 📚 **Referenz:** OWASP Top 10 for LLM Applications 2026 — [genai.owasp.org/llm-top-10](https://genai.owasp.org/llm-top-10/)

🎉 **MindfulChat geschafft!** Du hast jetzt praktisch erlebt, wie sich Prompt-Injection-Angriffe gegen ein LLM-System mit wachsender Verteidigung weiterentwickeln — genau das Wettrüsten, das reale AI-Security-Teams jeden Tag beschäftigt.

***

Weiter geht's mit einem ganz anderen Angriffsprofil — nicht Injection, sondern Rechte-Missbrauch: [**CorpConnect Messenger: Einführung**](corpconnect-messenger-einfuhrung.md).
