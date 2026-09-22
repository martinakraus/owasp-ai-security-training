# 📘 Über dieses Tutorial

## Learning by Hacking

Dieses GitBook ist als **Hands-On-Tutorial** aufgebaut — du liest nicht nur, du machst selbst mit. Jede Aufgaben-Seite folgt demselben Aufbau:

1. **Was ist neu?** — kurzer Kontext, was diese Aufgabe von der vorherigen unterscheidet
2. **Schritt-für-Schritt-Anleitung** — konkrete, nummerierte Schritte inklusive Beispiel-Payload zum Nachbauen
3. **Warum funktioniert das?** — eine ausführliche Erklärung des technischen Mechanismus dahinter, nicht nur "was" du eintippen musst

## ⚠️ Wichtig: Scores schwanken — das ist normal

Beim finalen Testdurchlauf haben wir eine wichtige Erkenntnis gewonnen, die du unbedingt kennen solltest, bevor du loslegst: **Die Ziel-Chatbots in Gandalf antworten nicht komplett deterministisch.** Derselbe oder ein sehr ähnlicher Payload kann bei unterschiedlichen Versuchen **stark unterschiedliche Scores** liefern — das liegt am zugrunde liegenden Sprachmodell selbst, nicht an einem Fehler in eurem Payload.

Konkret beobachtet beim Nachtesten dieses Tutorials:

| Level                 | Score bei Versuch 1 | Score bei Versuch 2 | Score bei Versuch 3 |
| --------------------- | ------------------- | ------------------- | ------------------- |
| MindfulChat Level 2   | 8                   | 62                  | **100**             |
| MindfulChat Level 3   | 16                  | 19                  | **100**             |
| Cycling Coach Level 2 | 6                   | 3                   | —                   |

**Was das für euch bedeutet:**

* Ein niedriger Score beim ersten Versuch heißt nicht, dass euer Payload falsch war — probiert ihn einfach noch ein- oder zweimal.
* Das gilt übrigens unabhängig von der Sprache: Wir haben denselben Payload auf Deutsch **und** Englisch getestet — die Sprache selbst war nicht der entscheidende Faktor für den Score, die Varianz zwischen Versuchen war deutlich größer als der Unterschied zwischen den Sprachen.
* Plant beim Timing im Workshop etwas Puffer ein, falls TN mehrere Anläufe brauchen — das ist kein Zeichen von "ich mach was falsch", sondern normales Verhalten der Plattform.

## Wie du es nutzen solltest

* **Selbst ausprobieren, bevor du weiterliest.** Der Lerneffekt ist am größten, wenn du erst 5–10 Minuten selbst experimentierst, bevor du dir die Musterlösung anschaust.
* **Es ist völlig ok, wenn etwas nicht klappt — auch beim zweiten Versuch nicht.** Gandalf passt seine Verteidigung von Level zu Level an, und die Antworten schwanken, wie oben beschrieben. Genau das macht den Lernprozess aus.
* **Die Erklärungen sind der eigentliche Punkt.** Eine Lösung abzutippen bringt wenig; verstehen, _warum_ ein Trick funktioniert, lässt sich auf ganz andere KI-Systeme übertragen.

> ⚠️ **Fair-Play-Hinweis:** Alle Techniken in diesem Tutorial richten sich ausschließlich gegen **Gandalf**, eine von Lakera öffentlich bereitgestellte, absichtlich verwundbare Übungsplattform. Wendet diese Techniken niemals gegen echte, produktive Systeme an, ohne dazu ausdrücklich autorisiert zu sein — das wäre unter anderem in den meisten Rechtsordnungen strafbar.

***

Als Nächstes: [**Vorbereitung & Agenda**](vorbereitung-and-agenda.md) — das Ziel für den heutigen Workshop.
