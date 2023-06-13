<!-- omit in toc -->
# Modul 114

## Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [Themenbereiche](#themenbereiche)
  - [Daten codieren](#daten-codieren)
    - [A.1 Zahlensysteme, numerische Codes](#a1-zahlensysteme-numerische-codes)
      - [Aufgabe zu Notepad++ und HxD](#aufgabe-zu-notepad-und-hxd)
    - [A.2 Alphanumerische Codes ASCII und Unicode](#a2-alphanumerische-codes-ascii-und-unicode)
    - [A.3 Zusammengesetzte Codierung, Barcodes](#a3-zusammengesetzte-codierung-barcodes)
    - [A.4 Bildcodierung](#a4-bildcodierung)
      - [RGB](#rgb)
      - [CMYK](#cmyk)
      - [YbcCr](#ybccr)
  - [Daten komprimieren](#daten-komprimieren)
    - [B.1 Verlustlose Komprimierung](#b1-verlustlose-komprimierung)
    - [B.2 Verlustbehaftete Komprimierung](#b2-verlustbehaftete-komprimierung)
  - [Grundlagen Kryptografie](#grundlagen-kryptografie)
    - [C.1 Symmetrische Verschlüsselung](#c1-symmetrische-verschlüsselung)
    - [C.2 Asymmetrische Verschlüsselung](#c2-asymmetrische-verschlüsselung)
    - [C.3 Digital signieren](#c3-digital-signieren)
  - [Gesicherte Datenübertragung](#gesicherte-datenübertragung)
    - [D.1 Public Key Infrastruktur](#d1-public-key-infrastruktur)
    - [D.2 Internet und Zertifikate](#d2-internet-und-zertifikate)
    - [D.3 PGP und OpenPGP](#d3-pgp-und-openpgp)
    - [D.4 Sichere E-Mails](#d4-sichere-e-mails)
- [Reflexion](#reflexion)
  - [Tag 1 (16.05.2023)](#tag-1-16052023)
  - [Tag 2 (23.05.2023)](#tag-2-23052023)
  - [Tag 3 (30.05.2023)](#tag-3-30052023)
  - [Tag 4 (06.06.2023)](#tag-4-06062023)
  - [Tag 5 (13.06.2023)](#tag-5-13062023)

## Themenbereiche

### Daten codieren

#### A.1 Zahlensysteme, numerische Codes

1. Ergänzen sie die folgende BIN-DEC-HEX-Zahlentabelle: (Was bedeutet MSB bzw. LSB?)

    - MSB: Most Significant Bit
    - LSB: Least Significant Bit

    |BIN(MSB)|BIN|BIN|BIN(LSB)|DEC|HEX|
    |:---|:---|:---|:---|---:|---:|
    | 0 | 0 | 0 | 0 | 0 | 0 |
    | 0 | 0 | 0 | 1 | 1 | 1 |
    | 0 | 0 | 1 | 0 | 2 | 2 |
    | 0 | 0 | 1 | 1 | 3 | 3 |
    | 0 | 1 | 0 | 0 | 4 | 4 |
    | 0 | 1 | 0 | 1 | 5 | 5 |
    | ... | ... | ... | ... | ... | ... |
    | 1 | 1 | 1 | 1 | 15 | F |

2. Wandeln sie die folgende Dezimalzahl ohne Taschenrechner in die entsprechende Binärzahl um: 911

   - 1110001111

3. Wandeln sie die folgende Binärzahl ohne Taschenrechner in die entsprechende Dezimalzahl um: 1011'0110

   - 182

4. Wandeln sie die folgende Binärzahl ohne Taschenrechner in die entsprechende Hexadezimalzahl um: 1110'0010'1010'0101

   - 58021

##### Aufgabe zu Notepad++ und HxD

`switzerland.bin` hat folgenden Inhalt:

```bin
°Eö
```

Das ist in HEX

```h
05 0B A1 45 12 1A 1F 9A
```

Folgende Zahlen lassen sich daraus extrahieren:

- `05 0B` -> `1291`: Bundesbrief der Schweiz
- `A1 45` -> `41285`: Fläche der Schweiz in km²
- `12 1A` -> `4643`: Dufourspitze
- `1F 9A` -> `8090`: PLZ der Behörden und Schulen in Zürich

#### A.2 Alphanumerische Codes ASCII und Unicode

- Welche der Dateien ist nun ASCII-codiert, welche UTF-8 und welche UTF-16 BE-BOM?

  - `Textsample1`: `ASCII`
  - `Textsample2`: `UTF-8`
  - `Textsample3`: `UTF-16 BE`

- Alle drei Dateien enthalten denselben Text. Aus wie vielen Zeichen besteht dieser?

  - 68

- Was sind die jeweiligen Dateigrössen? (Beachten sie, dass unter Grösse auf Datenträger jeweils 0 Bytes angegeben wird. Dies darum, weil beim Windows-Dateisystem NTFS kleine Dateien direkt in die MFT (Master File Table) geschrieben werden.) Wie erklären sie sich die Unterschiede?

  - Da ich ein UNIX-Basiertes Betriebssystem habe (MacOS), kann ich dies nicht beurteilen.

- Bei den weiteren Fragen interessieren uns nur noch die ASCII- und die UTF-8-Datei: Bekanntlich ist UTF-8 in den ersten 128 Zeichen deckungsgleich mit ASCII. Untersuchen sie nun die beiden HEX-Dumps und geben sie an, welche Zeichen unterschiedlich codiert sind. Ein kleiner Tipp: Es sind deren zwei.

  - `€` und `ä`

- Was bedeuten die beiden Ausdrücke, denen wir z.B. bei UTF-16 begegnen: Big-Endian (BE), Little-Endian (LE)?

  - Big-Endian (BE): Das höchstwertige Byte wird zuerst geschrieben.
  - Little-Endian (LE): Das niederstwertige Byte wird zuerst geschrieben.

- Im Notepad++ kann man unter dem Menüpunkt Codierung von ASCII zu UTF umschalten. Spielen sie damit etwas herum und notieren sie sich, was in der Darstellung jeweils ändert.

  - Je nach Kodierung ändern sich die Sonderzeichen, weil die Zeichentabellen anders interpretiert werden.

- Für Anspruchsvolle: Der UTF-8-Code kann je nach Zeichen ein, zwei, drei oder vier Byte lang sein. Wie kann der Textreader erkennen, wann ein UTF-8 Zeichencode beginnt und wann er endet? Untersuchen sie dies anhand der beiden Textsamples und lesen sie in z.B. Wikipedia die entsprechende Theorie zu UTF-8 durch. Tipp: Startbyte und Folgebyte.

#### A.3 Zusammengesetzte Codierung, Barcodes

> Keine Aufgaben thematisiert.

#### A.4 Bildcodierung

##### RGB

- `#FF0000` entspricht der Farbe -> rot
- `#00FF00` entspricht der Farbe -> grün
- `#0000FF` entspricht der Farbe -> blau
- `#FFFF00` entspricht der Farbe -> gelb
- `#00FFFF` entspricht der Farbe -> cyan
- `#FF00FF` entspricht der Farbe -> magenta
- `#000000` entspricht der Farbe -> schwarz
- `#FFFFFF` entspricht der Farbe -> weiss
- `#00BC00` entspricht der Farbe -> dunkel-grün

##### CMYK

- C:0%, M:100%, Y:100%, K:0%    entspricht der Farbe -> rot
- C:100%, M:0%, Y:100%, K:0%    entspricht der Farbe -> grün
- C:100%, M:100%, Y:0%, K:0%    entspricht der Farbe -> blau
- C:0%, M:0%, Y:100%, K:0%      entspricht der Farbe -> gelb
- C:100%, M:0%, Y:0%, K:0%      entspricht der Farbe -> cyan
- C:0%, M:100%, Y:0%, K:0%      entspricht der Farbe -> magenta
- C:100%, M:100%, Y:100%, K:0%  entspricht der Farbe -> schwarz (in theorie)
- C:0%, M:0%, Y:0%, K:100%      entspricht der Farbe -> schwarz
- C:0%, M:0%, Y:0%, K:0%        entspricht der Farbe -> weiss
- C:0%, M:46%, Y:38%, K:22%     entspricht der Farbe -> dunkeleres rot

##### YbcCr

- RGB 255/255/255           ergibt in YCbCr      -> 1, 0, 0
- RGB 0/0/0                 ergibt in YCbCr      -> 0, 0, 0
- Y:1, Cb:0, Cr:0           entspricht der Farbe -> weiss
- Y:0, Cb:0, Cr:0           entspricht der Farbe -> schwarz
- Y:0, Cb:1, Cr:0           entspricht der Farbe -> rot
- Y:0, Cb:-1, Cr:0          entspricht der Farbe -> grün
- Y:0, Cb:0, Cr:1           entspricht der Farbe -> blau
- Y:0, Cb:0, Cr:-1          entspricht der Farbe -> dunkel grün
- Y:0.3, Cb:0.5, Cr:-0.17   entspricht der Farbe -> rot(/braun, bäsch?)

### Daten komprimieren

#### B.1 Verlustlose Komprimierung

#### B.2 Verlustbehaftete Komprimierung

### Grundlagen Kryptografie

#### C.1 Symmetrische Verschlüsselung

#### C.2 Asymmetrische Verschlüsselung

#### C.3 Digital signieren

### Gesicherte Datenübertragung

#### D.1 Public Key Infrastruktur

#### D.2 Internet und Zertifikate

#### D.3 PGP und OpenPGP

#### D.4 Sichere E-Mails

## Reflexion

### Tag 1 (16.05.2023)

Heute haben wir uns intensiv mit Zahlensystemen und numerischen Codes im Modul 114 beschäftigt. Wir haben gelernt, wie unterschiedliche Zahlensysteme funktionieren.

Die letzte Aufgabe des Tages hat mir besonders gut gefallen und viel Spass gemacht. Es war eine anspruchsvolle Aufgabe, bei der ich meine Kenntnisse über Zahlensysteme und Codierung anwenden konnte. Es hat mich motiviert, meine Fähigkeiten weiterzuentwickeln.

Allerdings muss ich zugeben, dass es mir heute etwas schwergefallen ist, mich vollständig zu konzentrieren. Ich war heute ziemlich erschöpft und es war ein langer Tag. Trotzdem habe ich mein Bestes gegeben, um aktiv am Unterricht teilzunehmen und die Inhalte zu verstehen.

Ich freue mich aber schon auf das nächste Mal.

### Tag 2 (23.05.2023)

Der heutige Schultag zum Thema alphanumerische Codes ASCII und Unicode war lehrreich. Wir haben den ASCII-Code und seine Erweiterung gemäss ISO 8859 kennengelernt. Zudem haben wir die Notwendigkeit des Unicode zur Darstellung umfangreicherer Zeichensätze besprochen. Durch praktische Aufgaben haben wir die Unterschiede zwischen ASCII und UTF-8 erkundet und die Bedeutung von Big-Endian und Little-Endian erfahren. Insgesamt war der Schultag informativ und hat mein Verständnis für diese Codes erweitert.

### Tag 3 (30.05.2023)

> Krank

### Tag 4 (06.06.2023)

Heute hatten wir eine Prüfung über die bisherigen Themen. Die Fragen umfassten Zahlensysteme, Codes, Multimedia-Konzepte und Komprimierung. Die Prüfung hat mir geholfen, mein Verständnis zu überprüfen. Wir haben auch weitere interessante Themen behandelt, wie die Berechnung einer Videosequenz und den Huffman-Algorithmus. Insgesamt war der Tag lehrreich, und ich freue mich darauf, das Gelernte weiter anzuwenden.

