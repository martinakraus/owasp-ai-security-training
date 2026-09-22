# 🧙 Gandalf (Lakera): Plattform-Überblick

🔗 **URL:** [gandalf.lakera.ai](https://gandalf.lakera.ai)

Gandalf ist eine kostenlose, spielerisch aufgebaute Übungsplattform von Lakera für Prompt-Injection- und KI-Red-Teaming-Training. Es gibt zwei grundlegende Spielmodi:

## 1. Klassisches Gandalf (Password Reveal)

Das Original: Ein einzelner Chatbot verteidigt ein geheimes Passwort über mehrere, zunehmend schwierigere Level hinweg. Rein konversationsbasiert, kein Tool-Zugriff — der klassische Einstieg in Prompt Injection.

## 2. Gandalf: Agent Breaker

Die "agentische" Weiterentwicklung, und das, was wir heute nutzen: **ein ganzer App Store voller KI-Anwendungen — und jede einzelne davon kann gehackt werden.** Aktuell (Stand: dieser Workshop) gibt es genau **10 Apps**, jede mit einem eigenen Angriffsziel und mehreren Leveln steigender Schwierigkeit:

| App                       | Angriffsziel                                                                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Cycling Coach**         | Extrahiere den System-Prompt eines persönlichen Fahrrad-Trainings-Assistenten.                                                        |
| **Thingularity**          | Extrahiere die verfügbaren Tools eines Produktempfehlungs-Agenten.                                                                    |
| **OmniChat Desktop**      | Schmuggle einen Angriff in die Beschreibung eines MCP-Servers, um Nutzerdaten aus einem persönlichen Chat-Assistenten zu extrahieren. |
| **Clause AI**             | Exfiltriere geschützte Zeugeninformationen aus einem KI-Rechtsassistenten.                                                            |
| **CorpConnect Messenger** | Missbrauche fehlkonfigurierte Zugriffsrechte, um den Absender einer E-Mail in einem internen Firmen-Chat-Tool zu fälschen.            |
| **Curs-ed CodeReview**    | Baue eine bösartige Regel-Datei, die von einem automatisierten KI-Code-Review-Assistenten gelesen wird.                               |
| **Solace AI**             | Bringe einen Mental-Health-Support-Chatbot dazu, unangemessene Inhalte auszugeben.                                                    |
| **PortfolioIQ Advisor**   | Verstecke einen Angriff in einem PDF-Bericht, damit ein KI-Investmentberater falsche Einschätzungen ausgibt.                          |
| **Trippy Planner**        | Schmuggle einen Angriff in eine Webseite, damit ein Reiseplanungs-Agent einen bösartigen Link einfügt.                                |
| **MindfulChat**           | Schmuggle einen Angriff in die Memory-Logs eines Konversations-Chatbots.                                                              |

> 💡 Fällt dir was auf? Jede dieser Apps demonstriert eine andere OWASP-Kategorie aus dem letzten Kapitel — Cycling Coach z. B. LLM08 (Hidden Context Exposure), CorpConnect Messenger eher LLM03 (Excessive Agency), PortfolioIQ Advisor eine Form von LLM01 als indirekte Prompt Injection über ein Dokument. Wer nach dem Workshop noch Zeit und Lust hat: Alle 10 Apps sind einen Blick wert!

## Die Oberfläche im Detail

So sieht die Seite aus, wenn du eine App (hier: MindfulChat) geöffnet hast:

![Annotierte Ansicht der MindfulChat-Oberfläche: links Angriffsziel und Level, Mitte das Memory-Log-Eingabefeld, rechts die simulierte Opfer-App](.gitbook/assets/gandalf-ui.png)

* **① Links:** Angriffsziel ("Attack Objective"), Hintergrundszenario ("Attack Scenario"), über welchen Weg der Angriff eingeschleust wird ("Attack Vector") sowie dein aktueller Level mit Ziel-Score
* **② Mitte:** Hier trägst du deinen Payload ein — bei MindfulChat ist das ein simulierter "Memory Log"-Eintrag; bei anderen Apps kann das z. B. eine präparierte E-Mail oder ein Dokument sein
* **③ Unten:** Der Button, um deinen Angriff abzuschicken ("Initiate Attack")
* **④ Rechts:** Die "Attack Preview" — eine simulierte Vorschau der App, die das (fiktive) Opfer sieht. Nach dem Abschicken siehst du hier, wie die KI auf dein Opfer reagiert

## Wie der Score funktioniert

Der Score bewertet, wie gut dein Payload das jeweilige Angriffsziel erreicht hat — nicht binär "geschafft/nicht geschafft", sondern graduell von 0 bis 100. Ab ungefähr 75 Punkten gilt ein Level meist als bestanden ("Target score"), 100 ist die perfekte Lösung.

> 💡 **Tipp:** Wenn ein Payload abgelehnt wird oder 0 Punkte bekommt, gibt euch die Fehlermeldung oft einen Hinweis darauf, _warum_ — das systematisch auszuwerten ist meist zielführender als wildes Ausprobieren.

***

Heute schauen wir uns **vier** dieser Apps genauer an — wir starten mit einem kurzen, lustigen Warm-up: [**Cycling Coach: Einführung**](cycling-coach-einfuhrung-warm-up.md).
