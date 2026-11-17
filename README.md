**Emotionale Muster in Songtexten**



Dies ist eine NLP-Pipeline, welche Songtexte über die Genius-API sammelt, aufbereitet und mit zwei Ansätzen nach Themen bzgl. Emotionen klassifiziert. Zum einen ist das der regelbasierte Ansatz mit Vader (+ Schlüsselwörter) und der mit einem auf GoEmotions feinabgestimmten Transformer. Beide Ansätze werden gegen einen extern annotierten Benchmark (Malheiro et al. 2018) evaluiert.



Dieser Code entstand als Teil einer Gruppenarbeit im Kurs Informationslinguistik 2026 (Uni Regensburg)



Wir wollten herausfinden, ob sich Gefühle wie Herzschmerz, ästhetische Melancholie und mögliche Risikohinweise in Songtexten automatisch unterscheiden, und ob ein Transformer-Signal die Übereinstimmung mit einem externen Benchmark gegenüber einem rein regelbasiertem Ansatz verbessert.



Die **Pipeline** ist wie folgt aufgebaut:



01\_datensammlung: Songtexte über die API laden, Fehler protokollieren

01b\_benchmark\_daten: Benchmark laden, Stichprobe mit Songtexten anreichern

01c\_benchmark\_evaluation: Beide genannten Ansätze auf dem Benchmark klassifizieren und evaluieren

02\_vorberarbeitung: Bereinigung auf Song- und Abschnittsebene

03\_ansatz1\_regelbasiert\_vader: Vader Polarität pro Song

04\_ansatz2\_finetuned\_transformer: Emotionen mit roberta-base-go\_emotions

05\_risiko\_klassifikation: Zuordnung zu vier Kategorien, Aggregation von Abschnitten zu Songs

06\_playlist\_aggregation: Profile pro Playlist und Sensitivitätsanalyse zur Playlistgröße



Dabei liest jedes Notebook die Ausgabe des vorherigen. Somit kann sich auch jeder Schritt neu ausführen lassen.



**Methoden:**



\- Kategorien: kein\_hinweis, ästhetische\_melancholie, Herzschmerz, möglicher\_risikohinweis

\- Ansatz 1: Schlüsselwortlisten sind in fester Reihenfolge, Vader-Compound ist Rückfallregel

\- Ansatz 2: dieselben Schlüsselwörter ergänzt um due stärkste GoEmotions-Emotion in Kombi mit negativer Vader-Polarität

\- Abschnittsebene: Ein Song erhält die schwerste Kategorie, die in einem seiner Abschnitte vorkommt. Diese Entscheidung ist durchaus diskutierbar, da ein einzelner, auffälliger Chorus so sofort den ganzen Song einfärbt.

Evaluation: Die Benchmark-Quadranten nach Russell werden auf ein grobes Label abgebildet und mit den Ausgaben beider Ansätze verglichen.



**Daten und Urheberrecht:**



Die Songtexte sind urheberrechtlich geschützt und daher natürlich nicht Teil des Repos. Den Genius-Token kann man sich hier anlegen: https://genius.com/api-clients

Den Benchmark gibt es unter: http://mir.dei.uc.pt/downloads.html



*Malheiro, R., Panda, R., Gomes, P., \& Paiva, R. P. (2018). Emotionally-Relevant Features for Classification and Regression of Music Lyrics. IEEE Transactions on Affective Computing, 9(2), 240–254.*









