# Data Science in der Humanbiologie - Python Data Science Kurs

Willkommen zum Python Kurs **Data Science in der Humanbiologie**.

In diesem Kurs verwenden wir Python, um biologische Daten zu analysieren, zu visualisieren und wissenschaftlich auszuwerten.

Wir arbeiten mit:

- **Python** – Programmiersprache für Datenanalyse
- **Visual Studio Code (VS Code)** – Entwicklungsumgebung
- **Jupyter Notebooks** – interaktive Umgebung für Datenanalyse
- **Git** – zum Herunterladen und Aktualisieren der Kursmaterialien
- **uv** – Verwaltung der Python-Umgebung und benötigten Pakete

Die Installation muss nur **einmal vor Beginn des Praktikums** durchgeführt werden.

Bitte führe alle Schritte genau in der angegebenen Reihenfolge durch.

---

# Übersicht

Nach erfolgreicher Installation sieht dein Arbeitsablauf so aus:

```
GitHub Repository
        |
        ↓
Visual Studio Code
        |
        ↓
Python Umgebung (`.venv`)
        |
        ↓
+----------------+
|                |
VS Code      JupyterLab
|                |
+----------------+
        |
        ↓
Datenanalyse
```

---


# Voraussetzungen

Du benötigst:

☑ Computer mit Windows, macOS oder Linux
☑ Internetverbindung

Installiert werden:

☑ Visual Studio Code
☑ Git
☑ uv
☑ benötigte VS-Code-Erweiterungen

Die Python-Version und alle Python-Pakete werden automatisch durch `uv` verwaltet.

---

# Schritt 1 - Visual Studio Code installieren

Lade Visual Studio Code herunter:

[Visual Studio Code](https://code.visualstudio.com/)

Installiere VS Code mit den Standardeinstellungen.

Öffne VS Code nach der Installation einmal, um sicherzustellen, dass es funktioniert.

---

# Schritt 2 - Git installieren

Git benötigen wir, um die Kursmaterialien herunterzuladen und später zu aktualisieren.

Lade Git herunter:

[Git](https://git-scm.com/downloads)

Installiere Git mit den Standardeinstellungen.

---

## Git testen

Öffne ein Terminal.

### Windows

Öffne:

```
Startmenü → PowerShell
```

### macOS

Öffne:

```
Programme → Dienstprogramme → Terminal
```

### Linux

Öffne dein Terminal.

Gib ein:

```bash
git --version
```

Du solltest eine Ausgabe ähnlich dieser sehen:

```
git version 2.x.x
```

Wenn eine Versionsnummer erscheint, ist Git erfolgreich installiert.

---

# Schritt 3 - uv installieren

`uv` verwaltet die komplette Python-Umgebung für diesen Kurs.

Es:

* installiert die richtige Python-Version
* erstellt eine isolierte Umgebung
* installiert alle benötigten Pakete
* sorgt dafür, dass alle Studierenden dieselbe Umgebung verwenden

---

## Windows

Öffne PowerShell:

```powershell
winget install --id=astral-sh.uv
```

---

## macOS und Linux

Öffne ein Terminal:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Falls unter Linux `curl` fehlt:

```bash
sudo apt install curl -y
```

---

Schließe danach das Terminal vollständig und öffne ein neues Terminal.

Teste:

```bash
uv --version
```

Beispiel:

```
uv 0.x.x
```

---

# Schritt 4 - VS Code Erweiterungen installieren

Öffne VS Code.

Klicke links auf das Symbol "Extensions":

![Extensions](assets/extensions.svg)

Installiere die folgenden Erweiterungen:


| Erweiterung | Publisher | Extension ID (Suchbegriff) | Zweck |
|---|---|---|---|
| Python | Microsoft | `ms-python.python` | Python-Unterstützung, Interpreter auswählen, Ausführen von Python-Code |
| Jupyter | Microsoft | `ms-toolsai.jupyter` | Öffnen und Ausführen von Jupyter Notebooks (`.ipynb`) |
| Data Wrangler | Microsoft | `ms-toolsai.datawrangler` | Interaktive Untersuchung und Aufbereitung von Datensätzen |
| Ruff | Astral Software | `charliermarsh.ruff` | Automatische Code-Analyse und Formatierung |

---


# Schritt 5 - Kursmaterialien herunterladen

Öffne ein Terminal.

Wechsle an den Ort, an dem du den Kurs speichern möchtest.

Beispiel:

```bash
cd Documents
```

Lade das Repository herunter:

```bash
git clone https://github.com/MarcoMernberger/data_science_human_biology.git
```

Wechsle in den Kursordner:

```bash
cd data_science_human_biology
```

Prüfe den Inhalt:

Linux oder macOS:

```bash
ls -al
```

Windows:

```powershell
dir
```

Du solltest unter anderem sehen:

```
README.md
pyproject.toml
uv.lock
notebooks
data
```

---


# Schritt 6 - Python-Umgebung erstellen

Im Kursordner führst du aus:

```bash
uv sync
```

Dieser Befehl:

- erstellt eine eigene Python-Umgebung
- installiert alle benötigten Python-Pakete
- installiert exakt die Versionen, die im Kurs verwendet werden

Die erste Installation kann einige Minuten dauern.

Nach erfolgreicher Installation existiert ein neuer Ordner:

```
.venv
```

Dieser Ordner enthält deine Kursumgebung.

Bitte lösche oder verändere diesen Ordner nicht.

---

# Schritt 7 - Kurs in VS Code öffnen

Im Terminal:

```bash
code .
```

Alternativ:

1. Öffne VS Code
2. Wähle:

```
Datei → Ordner öffnen
```

3. Wähle:

```
data_science_human_biology
```

---

# Schritt 8 - Python-Umgebung in VS Code auswählen

VS Code muss wissen, welche Python-Version verwendet werden soll.

Drücke:

## Windows/Linux

```
Ctrl + Shift + P
```

## macOS

```
Cmd + Shift + P
```

Suche:

```
Python: Select Interpreter
```

Wähle:

```
Python 3.13 (`.venv`)
```

bzw. den Interpreter aus dem Ordner:

```
.venv
```

![Select Python Interpreter](assets/select_interpreter.svg)

---

# Schritt 9 - Jupyter lab testen

VScode kann je nach Menge der installierten Extensions und Resourcen euren Rechner ganz gut auslasten. 

Falls VS Code auf deinem Rechner langsam läuft, kann der Kurs auch direkt mit JupyterLab bearbeitet werden.

JupyterLab läuft im Webbrowser und benötigt weniger Ressourcen als eine vollständige Entwicklungsumgebung.


## JupyterLab starten

Öffne ein Terminal im Kursordner:

```bash
uv run jupyter lab
```

Es öffnet sich automatisch ein Browserfenster mit JupyterLab.

Falls kein Browser automatisch startet, kopiere die angezeigte URL in den Browser.

Beispiel:

[http://localhost:8888/lab](http://localhost:8888/lab)

## JupyterLab beenden

Im Terminal:

`Ctrl + C`

---


# Schritt 10 - Installation testen

Öffne:

```
notebooks/00_setup_test.ipynb
```

Oben rechts im Notebook:

Wähle den Kernel:

```
Python (`.venv`)
```

![Select Kernel](assets/select_kernel.svg)


Klicke anschließend:

```
Run All
```

Das Notebook sollte ohne Fehlermeldungen durchlaufen.

Am Ende muss die grüne Erfolgsmeldung erscheinen und der Testplot muss sichtbar sein.

Wenn du die Grafik siehst:

🎉 Deine Python-Umgebung ist erfolgreich eingerichtet.

---


# Arbeiten während des Kurses

## Notebook öffnen

Die Kursübungen befinden sich in Dateien mit der Endung:

```
.ipynb
```

Diese Dateien werden direkt in VS Code geöffnet.

Code wird über die ▶-Schaltfläche ausgeführt.

---

# Kursmaterialien aktualisieren

Wenn neue oder aktualisierte Materialien bereitgestellt werden sollten:

Öffne ein Terminal im Kursordner und führe aus:

```bash
git pull
```

---

# Python-Pakete aktualisieren

Die Kursumgebung wird zentral über `pyproject.toml` und `uv.lock` verwaltet.

Falls neue Python-Pakete zum Kurs hinzugefügt werden, werden diese über das Kursrepository bereitgestellt.

Nach einer Aktualisierung der Kursmaterialien:

```bash
git pull
uv sync
```

# Eigene Python-Pakete hinzufügen

Solltet ihr später eigene Pakete installieren wollen, geht das über:

```bash
uv add <package>
```

Dadurch werden automatisch pyproject.toml und uv.lock aktualisiert.

Wenn ihr ein eigenes Projekt entwickelt und es mit anderen teilen möchtet, müssen beide Dateien mitgegeben werden:

```
pyproject.toml
uv.lock
```

---

# Wichtige Regeln

## Keine Pakete selbst auf anderem Weg installieren!

Bitte nicht verwenden:

```bash
pip install <paketname>
```

Die Kursumgebung wird automatisch über diese Dateien verwaltet:

```
pyproject.toml
```

und

```
uv.lock
```

Manuelle Installationen können zu Problemen führen.

---

## Den Ordner .venv nicht löschen

Der Ordner:

```
.venv
```

enthält deine persönliche Python-Umgebung für diesen Kurs.

---

# Fehlerbehebung

## Problem: VS Code findet Python nicht

Öffne die Befehlspalette:

Windows/Linux:

```
Ctrl + Shift + P
```

macOS:

```
Cmd + Shift + P
```

Wähle:

```
Python: Select Interpreter
```

und anschließend:

```
.venv
```

---

## Problem: Etwas funktioniert nicht

Versuche zuerst:

```bash
uv sync
```

und starte VS Code neu.

Falls das Problem weiterhin besteht, notiere:

1. Betriebssystem:
   - Windows
   - macOS
   - Linux

2. Den ausgeführten Befehl

3. Die vollständige Fehlermeldung

---

# Checkliste vor Beginn des Praktikums

Vor dem Praktikum sollte alles Folgende erledigt sein:

☑ VS Code installiert  

☑ Git installiert  

☑ uv installiert  

☑ Python VS Code Extension installiert  

☑ Jupyter VS Code Extension installiert  

☑ Kursrepository heruntergeladen  

☑ `uv sync` erfolgreich ausgeführt  

☑ VS Code und jupyter lab einmal gestartet

☑ Test-Notebook erfolgreich ausgeführt  

Du bist jetzt bereit für den Kurs!