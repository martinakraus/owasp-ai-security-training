# 🧠 Was ist AI Security — und warum jetzt?

## Fangen wir ganz von vorne an: Was ist eigentlich ein LLM?

Bevor wir über _Sicherheit_ sprechen, lohnt sich ein kurzer Blick darauf, was ein KI-Chatbot wie ChatGPT, Claude oder Gemini technisch überhaupt ist — denn genau darin steckt später auch die Schwachstelle.

Ein **LLM (Large Language Model)** ist im Kern eine sehr große "Vorhersage-Maschine" für Text. Beim Training bekommt das Modell riesige Mengen an Text zu lesen (Bücher, Webseiten, Artikel) und lernt dabei ein Muster: _Welches Wort (genauer: welches "Token", ein Wort- oder Wortteil-Baustein) folgt statistisch am wahrscheinlichsten auf die bisherigen Wörter?_ Wenn du also mit einem LLM chattest, passiert im Kern immer dasselbe: Das Modell bekommt den bisherigen Text und berechnet, welches nächste Wort am plausibelsten ist — das macht es Wort für Wort, bis eine vollständige Antwort entsteht.

Wichtig zu verstehen: Ein LLM "versteht" nicht im menschlichen Sinne und hat auch kein festes Gedächtnis wie ein Mensch. Es reagiert ausschließlich auf den Text, den es in dem Moment vor sich hat. Genau dieser Text heißt **Kontext**, und wie der zustande kommt, schauen wir uns gleich an.

## Was ist ein Prompt?

Ein **Prompt** ist einfach die Eingabe, die du an ein LLM schickst — zum Beispiel die Frage, die du in ein Chat-Fenster tippst. Das Modell nimmt deinen Prompt, hängt ihn an den bisherigen Gesprächsverlauf an und berechnet daraus seine Antwort.

Beispiel: Du tippst "Was ist die Hauptstadt von Frankreich?" — das ist dein Prompt. Das Modell berechnet daraus die wahrscheinlichste Fortsetzung: "Die Hauptstadt von Frankreich ist Paris."

## Was ist ein System Prompt?

Wenn eine Firma einen Chatbot baut (z. B. einen Kundensupport-Bot), möchte sie dem Modell meist ein paar Grundregeln mitgeben, bevor die Nutzer:innen überhaupt etwas eintippen. Das nennt man **System Prompt**. Ein Beispiel:

```
Du bist der Support-Assistent von ExampleShop. Beantworte nur
Fragen zu Bestellungen und Rückgaben. Gib niemals interne
Preiskalkulationen preis.
```

Dieser System Prompt ist für Nutzer:innen normalerweise unsichtbar — er wird im Hintergrund vor jede Unterhaltung gesetzt.

## Das Kontextfenster: Der entscheidende Punkt für alles, was folgt

Jetzt kommt der wichtigste Baustein für das gesamte Thema KI-Security: Wenn das Modell eine Antwort berechnet, bekommt es nicht nur deinen einen Prompt — es bekommt den **gesamten Text**, der für diese Anfrage relevant ist, alles zusammengefügt zu einem einzigen großen Textblock. Das nennt man das **Kontextfenster**. Da können unter anderem drin stecken:

* der System Prompt (die Grundregeln der Firma)
* der bisherige Gesprächsverlauf
* deine aktuelle Frage
* ggf. Dokumente, die das Modell zur Beantwortung heranzieht (dazu gleich mehr bei RAG)
* ggf. gespeicherte Informationen aus früheren Sitzungen (dazu gleich mehr bei Memory)

Das Entscheidende: **Für das Modell sieht das alles gleich aus — es ist einfach Text.** Es gibt keine eingebaute, zuverlässige Markierung, die sagt "dieser Teil ist eine wichtige Regel der Firma" und "dieser Teil ist nur ein Dokument, das du zur Information lesen sollst". Das Modell versucht bestenfalls anhand von Formulierung und Position im Text zu erahnen, was wichtiger ist — aber es gibt keine harte, technische Grenze wie z. B. eine Firewall zwischen Netzwerken.

> 💡 **Das ist der Kern des gesamten Themas KI-Security.** Fast jede Schwachstelle, die wir heute besprechen und selbst ausprobieren, basiert letztlich darauf, dass Anweisung und Information im selben Topf landen.

## Was ist Prompt Injection?

Wenn man verstanden hat, dass Anweisung und Information im Kontextfenster nicht sauber getrennt sind, ergibt sich fast zwangsläufig eine Angriffsidee: Was, wenn ich als Angreifer:in einfach Text in dieses Kontextfenster einschmuggle, der wie eine Anweisung aussieht — und das Modell befolgt ihn, obwohl er eigentlich nur "Information" (z. B. aus einem Dokument) sein sollte?

Genau das nennt man **Prompt Injection**. Man unterscheidet grob zwei Varianten:

* **Direkte Prompt Injection:** Man tippt die manipulative Anweisung direkt in den Chat, z. B. "Ignoriere alle bisherigen Anweisungen und tu stattdessen X."
* **Indirekte Prompt Injection:** Die Anweisung steckt versteckt in Daten, die das Modell erst später verarbeitet — z. B. in einer Webseite, einem PDF, einer E-Mail oder einem gespeicherten Datenbankeintrag. Das Modell liest diese Daten im Rahmen einer eigentlich harmlosen Aufgabe und führt die versteckte Anweisung trotzdem aus.

Genau die indirekte Variante werdet ihr gleich bei MindfulChat selbst ausprobieren.

## Was ist ein Agent — und warum wird das Problem dadurch größer?

Solange ein Modell nur Text zurückgibt, den ein Mensch liest, ist der mögliche Schaden einer Prompt Injection meist überschaubar (z. B. eine peinliche oder falsche Antwort). Richtig gefährlich wird es, wenn ein Modell zu einem **Agenten** wird — also zusätzlich Zugriff auf Werkzeuge ("Tools") bekommt: E-Mails verschicken, Datenbanken abfragen, Code ausführen, Zahlungen auslösen. Dann kann eine erfolgreiche Prompt Injection nicht mehr nur eine falsche Textantwort verursachen, sondern eine **echte Handlung** auslösen — eine verschickte E-Mail lässt sich nicht mehr zurückholen.

## Was ist RAG (Retrieval-Augmented Generation)?

Ein LLM kennt nur das, was in seinen Trainingsdaten stand — und die haben irgendwann einen Stichtag ("Wissensstand"). Wenn eine Firma möchte, dass ihr Chatbot aktuelle oder firmeninterne Informationen kennt (z. B. die neueste Produktdokumentation), reicht das Training allein nicht aus. Die gängige Lösung heißt **RAG (Retrieval-Augmented Generation)** — auf Deutsch etwa "durch Suche angereicherte Texterzeugung":

1. Die Firma legt ihre Dokumente (Handbücher, FAQs, Richtlinien) in einer durchsuchbaren Datenbank ab.
2. Wenn jemand eine Frage stellt, sucht das System zuerst die inhaltlich passendsten Dokument-Ausschnitte heraus ("Retrieval" = Abrufen).
3. Diese Ausschnitte werden **in das Kontextfenster** eingefügt, zusammen mit der eigentlichen Frage.
4. Das Modell formuliert die Antwort dann auf Basis dieser eingefügten Informationen ("Generation" = Erzeugen).

Das Problem für die Sicherheit: Schritt 3 bedeutet, dass fremder Text (aus einem Dokument, das vielleicht nicht einmal von der eigenen Firma stammt) direkt in denselben Kontext wandert wie die Systemregeln. Steckt in einem dieser Dokumente eine versteckte Anweisung, landet sie im selben ungeschützten Topf, den wir oben beschrieben haben. Das nennt man **RAG-Poisoning**, wenn jemand gezielt vergiftete Dokumente in so eine Wissensdatenbank einschleust.

## Was ist "Memory" bei einem KI-Assistenten?

Viele moderne KI-Assistenten sollen sich "an dich erinnern" — z. B. deine Vorlieben aus früheren Gesprächen. Damit das über eine einzelne Unterhaltung hinaus funktioniert, speichert das System Notizen (z. B. "Nutzer mag italienisches Essen") in einer Datenbank und fügt sie bei zukünftigen Gesprächen wieder in den Kontext ein — technisch also ein Spezialfall von RAG, nur eben mit Notizen über dich statt mit Firmendokumenten. Auch hier gilt: **Wenn jemand einen gefälschten Eintrag in diese Memory-Datenbank einschleusen kann, landet auch der ungeschützt im Kontext des Modells.** Genau dieses Prinzip ist die Grundlage von MindfulChat, das ihr gleich selbst ausprobiert.

## Warum ist das Thema gerade jetzt so relevant?

Vor wenigen Jahren waren LLMs vor allem Chat-Spielereien ohne Tool-Zugriff. Heute stecken sie als Agenten mit RAG-Anbindung und Memory in Kundensupport, Coding-Assistenten und internen Unternehmenssystemen. Jede dieser zusätzlichen Fähigkeiten — Tools, RAG, Memory — vergrößert die Angriffsfläche, wie du jetzt nachvollziehen kannst. Und weil das zugrunde liegende Problem (keine saubere Trennung von Anweisung und Information) bisher **nicht zuverlässig lösbar** ist, wächst mit der Verbreitung von KI-Systemen auch die Zahl realer Sicherheitsvorfälle.

## Mini-Glossar zum Nachschlagen

| Begriff              | Kurz erklärt                                                                                                                                                  |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **LLM**              | KI-Modell, das durch Training auf Text lernt, plausible Text-Fortsetzungen zu berechnen.                                                                      |
| **Prompt**           | Die Eingabe, die an ein LLM geschickt wird.                                                                                                                   |
| **System Prompt**    | Unsichtbare Grundregeln, die einem Modell vor dem Gespräch mitgegeben werden.                                                                                 |
| **Kontextfenster**   | Der gesamte Text (System Prompt + Verlauf + Daten), den das Modell bei einer Antwort berücksichtigt — ohne harte Trennung zwischen Anweisung und Information. |
| **Prompt Injection** | Angriff, der über geschickt platzierten Text eine ungewollte Anweisung ins Kontextfenster schmuggelt.                                                         |
| **Agent**            | Ein LLM mit Zugriff auf Werkzeuge, das selbstständig Aktionen ausführen kann.                                                                                 |
| **RAG**              | Verfahren, bei dem passende Dokument-Ausschnitte automatisch in den Kontext eingefügt werden, um aktuelles/internes Wissen bereitzustellen.                   |
| **Memory**           | Gespeicherte Notizen über frühere Gespräche, die in späteren Sitzungen wieder in den Kontext eingefügt werden.                                                |

***

Auf der nächsten Seite schauen wir uns an, wie die Sicherheits-Community diese Risiken systematisch kategorisiert: die [**OWASP Top 10 für LLM-Anwendungen**](bedrohungsubersicht-owasp-top-10-fur-llm-anwendungen-2026.md).
