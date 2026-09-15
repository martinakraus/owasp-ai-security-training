# 🎯 MindfulChat — Level 6 & 7

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

🎉 **MindfulChat geschafft!** Du hast jetzt praktisch erlebt, wie sich Prompt-Injection-Angriffe gegen ein LLM-System mit wachsender Verteidigung weiterentwickeln — genau das Wettrüsten, das reale AI-Security-Teams jeden Tag beschäftigt.

***

Weiter geht's mit einem ganz anderen Angriffsprofil — nicht Injection, sondern Rechte-Missbrauch: [**CorpConnect Messenger: Einführung**](corpconnect-messenger-einfuhrung.md).
