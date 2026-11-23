# THES4INTWIRE – Bedienungsanleitung

> **Version 1.24.0 · Windows 11 x64 · Freeware (Closed Source)**  
> © 2026 TheS4int · *Every Packet Tells a Story.*

Diese Anleitung beschreibt die Bedienung des Netzwerk- und Security-Monitors THES4INTWIRE. Sie erklärt die Funktionen, ihre Messgrenzen und typische Probleme. **Ein fehlender Sicherheitsfund bedeutet nicht, dass eine Verbindung sicher ist.**

## Inhaltsverzeichnis

1. [Installation und erster Start](#1-installation-und-erster-start)
2. [Netzwerk-Live-Monitor](#2-netzwerk-live-monitor)
3. [Performance und Paketdaten](#3-performance-und-paketdaten)
4. [Prozesse und Netzwerkverbindungen](#4-prozesse-und-netzwerkverbindungen)
5. [Browser Intelligence und Tab-Traffic](#5-browser-intelligence-und-tab-traffic)
6. [Threat Intelligence und lokale IOC-Liste](#6-threat-intelligence-und-lokale-ioc-liste)
7. [VirusTotal und AbuseIPDB](#7-virustotal-und-abuseipdb)
8. [Oberfläche, Mini-Fenster und Tray](#8-oberfläche-mini-fenster-und-tray)
9. [Fehlerbehebung](#9-fehlerbehebung)
10. [Glossar](#10-glossar)

---

## 1. Installation und erster Start

1. Auf der [Releases-Seite](../../releases) die passende **Windows-Release-Datei** herunterladen. **Nicht** die automatisch von GitHub erzeugten Archive „Source code (zip/tar.gz)“ als Windows-Programm verwenden.
2. Die portable ZIP-Datei entpacken und die darin enthaltene `thes4intwire.exe` starten.
3. Im oberen Bereich bei Bedarf einen **Netzwerkadapter** auswählen. **Alle Adapter** fasst die überwachten Schnittstellen zusammen.
4. Die Anzeigeeinheit (z. B. Mbit/s oder MB/s) auswählen und den Live-Verlauf prüfen.

**Systemhinweise:** Windows 11 x64 ist das primäre Zielsystem. Die Anwendung benötigt die Microsoft Edge WebView2 Runtime. Bestimmte ETW-Messungen können von Windows-Berechtigungen und laufenden ETW-Sitzungen abhängen. Unternehmensrichtlinien beachten; Sicherheitswarnungen nicht ungeprüft übergehen.

## 2. Netzwerk-Live-Monitor

Auf der **Übersicht** zeigt THES4INTWIRE den ein- und ausgehenden Netzwerkverkehr als Live-Werte und Graphen.

| Anzeige | Bedeutung |
| --- | --- |
| **↓ Download** | Empfangsrate des überwachten Adapters bzw. der überwachten Adapter |
| **↑ Upload** | Senderate |
| **RX Pakete/s** | Empfangene Pakete pro Sekunde |
| **TX Pakete/s** | Gesendete Pakete pro Sekunde |
| **Adapterauswahl** | Eingrenzung auf die gewünschte Netzwerkschnittstelle |
| **Pause** | Hält die dargestellte Live-Aktualisierung an |

**Hinweis:** Die Adapter-Gesamtrate ist nicht automatisch mit der Summe einzelner Prozess- oder Browser-Tab-Werte identisch. Verschiedene Datenquellen erfassen unterschiedliche Ebenen des Netzwerkverkehrs.

## 3. Performance und Paketdaten

Im Menü **Performance** lassen sich Verlaufskurven und Paketaktivität beobachten. In der Übersicht zeigen getrennte Kurven bzw. Kennzeichnungen die Richtungen **Download** und **Upload**. Einheiten vor Vergleichen kontrollieren.

Bei sehr kleinen Werten kann die Kurve nahe null liegen. Kurze Spitzen sind nicht automatisch verdächtig: Downloads, Videostreams, Updates und Hintergrunddienste können starke Ausschläge verursachen.

## 4. Prozesse und Netzwerkverbindungen

Unter **Prozesse & Verbindungen** werden erkannte Windows-Endpunkte einschließlich Prozesszuordnung angezeigt.

Typische Spalten:

- **Prozess / PID:** ausführbares Programm und Windows-Prozesskennung
- **Protokoll / Status:** z. B. TCP4, TCP6, UDP, ESTABLISHED oder FIN_WAIT_1
- **Lokaler Port:** Port auf deinem Rechner
- **Ziel-IP : Port:** Gegenstelle und deren Port
- **Hostname (PTR):** optionaler Reverse-DNS-Eintrag
- **Netzbetreiber (RDAP):** registrierter IP-Netzinhaber, sofern ermittelbar
- **Download / Upload je Prozess bzw. Verbindung:** ETW-Messwerte, wenn Windows passende Ereignisse liefert

### PTR und RDAP verwenden

1. Bei einer Ziel-IP **PTR suchen** klicken, um einen Reverse-DNS-Namen abzufragen.
2. Über **RDAP suchen** den registrierten Netzbetreiber abrufen.
3. Ergebnisse als **Hinweise**, nicht als Identitätsnachweis der besuchten Website verstehen.

**Beispiel:** `bc.googleusercontent.com` kann zu Cloud-Infrastruktur gehören. Das beweist nicht, welche konkrete Website ein Programm aufgerufen hat. **„Kein PTR-Eintrag“ ist kein Verbindungsfehler.**

### ETW-Bandbreitenmessung

ETW (*Event Tracing for Windows*) kann Prozess- und Ziel-IP-Verkehr liefern. Die Messung hängt von den durch Windows bereitgestellten Ereignissen ab; nicht jeder Verbindungseintrag erzeugt jederzeit messbare Daten. Die Anzeige **ETW neu starten** startet die Sitzung erneut. Mehrfach gestartete THES4INTWIRE-Instanzen vermeiden.

## 5. Browser Intelligence und Tab-Traffic

THES4INTWIRE unterstützt eine optionale lokale **Browser Bridge** für:

| Browser | Tab-Anzeige | Tab-Traffic |
| --- | --- | --- |
| Google Chrome | Ja | Beobachtete Browser-Netzwerkdaten (Debugger-Berechtigung) |
| Microsoft Edge | Ja | Beobachtete Browser-Netzwerkdaten (Debugger-Berechtigung) |
| Brave | Ja | Beobachtete Browser-Netzwerkdaten (Debugger-Berechtigung) |
| Opera | Ja | Beobachtete Browser-Netzwerkdaten (Debugger-Berechtigung) |
| Mozilla Firefox | Ja | Empfangene HTTP-Antwortdaten; Upload nicht verfügbar |
| Tor Browser | Keine Tab-Erfassung | Keine Tab-Erfassung |

### Browser Bridge einrichten

1. THES4INTWIRE öffnen → **Prozesse & Verbindungen** → **Pairing-Code anzeigen**.
2. Das **separate Browser-Bridge-Paket** aus den Release-Assets herunterladen und entpacken.
3. Bei **Chrome, Edge, Brave oder Opera** die jeweilige Erweiterungsseite öffnen (`chrome://extensions`, `edge://extensions`, `brave://extensions`, `opera://extensions`), den Entwicklermodus einschalten und den Ordner `browser-extensions/chromium` als entpackte Erweiterung laden.
4. Bei **Firefox** `about:debugging#/runtime/this-firefox` öffnen und `browser-extensions/firefox/manifest.json` als **temporäres Add-on** laden. Dieses bleibt nach einem Neustart nicht installiert.
5. Im Optionsfenster der Erweiterung den Browser auswählen, den Pairing-Code einfügen und speichern.
6. Einen normalen Webseiten-Tab öffnen oder neu laden. Anschließend die Tab-Liste in THES4INTWIRE prüfen.

**Wichtig:** Chromium-basierte Browser können während der Tab-Traffic-Messung eine Meldung anzeigen wie **„Debugging dieses Tabs durch THES4INTWIRE Browser Bridge wird ausgeführt“**. Diese vom Browser erzeugte Sicherheitsleiste ist eine Folge der Debugger-Schnittstelle und lässt sich über THES4INTWIRE nicht seriös unterdrücken. Beim Trennen der Debugger-Verbindung entfällt die entsprechende Detailmessung.

### Bedeutung der Tab-Traffic-Spalten

- **↓ Download:** browserseitig beobachtete Empfangsbytes/Rate für erfasste Anfragen des Tabs.
- **↑ Upload:** nur beobachtbare Request-Body-Daten; **kein** vollständiger TCP-/TLS-Upload.
- **—:** Daten fehlen oder können mit dem jeweiligen Browser nicht erfasst werden.
- **0:** Aus dieser Datenquelle wurden keine Bytes gezählt; das ist nicht immer gleichbedeutend mit null Netzwerkverkehr.

Eine Tab-Liste allein weist nicht nach, welcher Tab eine bestimmte TCP-Verbindung verursacht hat. Browser- und ETW-Werte dürfen nicht ohne Weiteres addiert werden. Browser-Titel und bereinigte URLs werden an einen **lokalen** Listener auf `127.0.0.1:38471` übertragen; regulär keine privaten Fenster.

**Weitere Einzelanleitungen:** [Browser einrichten](docs/BROWSER-SETUP-DE.md) · [Tab-Traffic und Messgrenzen](docs/TAB-TRAFFIC-DE.md)

## 6. Threat Intelligence und lokale IOC-Liste

Das **Threat Intelligence // Local IOC Center** gleicht die aktuell beobachteten externen Prozessverbindungen mit einer **selbst gepflegten lokalen Watchlist** ab.

### Eigene IOC-Liste verwenden

1. Menü **Threat Intelligence** öffnen.
2. Im Bereich für die lokale IOC-Liste je Zeile eine IP-Adresse oder ein IPv4-CIDR-Netz mit optionaler Beschreibung eingeben, z. B.:

   ```text
   203.0.113.10 | Dokumentationsbeispiel, kein echter Bedrohungsindikator
   198.51.100.0/24 | Beispielnetz, keine echte Blockliste
   ```

3. **IOC-Liste speichern** anklicken.
4. **Lokal analysieren** beziehungsweise **Jetzt analysieren** ausführen.
5. In der Tabelle nach **IOC-Treffer** oder Prozess/IP suchen.

Die oben gezeigten reservierten Dokumentationsadressen dienen nur zur Erläuterung und erzeugen normalerweise **keinen Treffer**, weil sie keine realen öffentlichen Verbindungsziele sind. Zum Funktionstest nur eine bewusst selbst ausgewählte und dokumentierte Ziel-IP verwenden; einen Testtreffer danach wieder entfernen.

### Bewertung verstehen

| Anzeige | Aussage |
| --- | --- |
| **NICHT BEWERTET** | Kein verwertbarer Reputationsbericht und kein lokaler Treffer |
| **IOC-TREFFER** | Übereinstimmung mit deiner eigenen IOC-Liste; **keine automatische Malware-Bestätigung** |
| **KEIN HINWEIS** | Ein Anbieter lieferte Daten, aber der konfigurierte Schwellenwert wurde nicht überschritten |
| **PRÜFEN** | Mindestens ein verdächtiger/malicious VirusTotal-Hinweis oder AbuseIPDB-Confidence ≥ 25 |
| **HOHER HINWEIS** | Mindestens 3 VirusTotal-malicious-Meldungen oder AbuseIPDB-Confidence ≥ 80 |

Das Center **blockiert keine Prozesse oder Netzwerkziele**. Weitere Details: [Lokale IOC-Analyse](docs/THREAT-INTELLIGENCE-DE.md).

## 7. VirusTotal und AbuseIPDB

Die Online-Reputation ergänzt die lokale Watchlist. Für jeden Dienst ist ein eigener API-Schlüssel erforderlich.

1. Im Bereich **Threat Intelligence** einen VirusTotal- und/oder AbuseIPDB-API-Schlüssel eintragen.
2. Für die ausschließlich lokale Prüfung auf **Lokal analysieren** klicken.
3. Mit **Online-Reputation prüfen** die gezielte externe Abfrage starten.
4. Die Tabelle zeigt unter anderem **VirusTotal malicious/suspicious**, **AbuseIPDB Confidence/Reports**, Prüfzeit und eine abgeleitete Priorität.

**Limit pro Durchlauf:** Die Anwendung fragt höchstens **drei unterschiedliche öffentliche IP-Adressen** pro Klick ab; die Reihenfolge beruht auf der beobachteten Verbindungsliste, nicht auf einer Vorab-Risikobewertung. Bereits erfolgreich überprüfte IPs können übersprungen werden.

**Hinweis-Index (0–100):** Eine *Heuristik zur Priorisierung*, **keine prozentuale Wahrscheinlichkeit einer Infektion**. Lokaler IOC-Treffer: 100. Andernfalls der höhere Wert aus `min(100, 20 × VT malicious + 8 × VT suspicious)` und `AbuseIPDB Confidence`. Ohne verwertbaren Bericht wird `—` angezeigt.

**Datenschutz:** Die abgefragte öffentliche IP wird beim Online-Check an den jeweiligen Dienst übertragen. VirusTotal kann Indikatoren in seiner Datenbasis erfassen. Keine vertraulichen Umgebungsdaten ungeprüft übertragen. API-Limits und Nutzungsbedingungen des jeweiligen Dienstes beachten. In v1.24 werden API-Schlüssel nicht dauerhaft gespeichert.

Mehr: [Einrichtung der Online-Reputation](docs/REPUTATION-SETUP-DE.md).

## 8. Oberfläche, Mini-Fenster und Tray

- **Skin: Neon / Noir Neon:** Anzeige zwischen den verfügbaren Designs umschalten.
- **Mini-Fenster:** kompakte Darstellung der Netzwerkwerte.
- **Immer oben:** das Fenster vor anderen Fenstern halten.
- **Pause:** sichtbare Live-Aktualisierung anhalten.
- **Tray:** Anwendung über das Benachrichtigungsfeld verwalten bzw. regulär beenden.

Breite Prozesstabellen und Browser-Listen können bei schmalem Fenster **horizontal scrollbar** sein. Bei Windows-Anzeigeskalierung Fenster gegebenenfalls vergrößern und seitlich scrollen, statt abgeschnittene Werte anzunehmen.

## 9. Fehlerbehebung

| Problem | Prüfschritte |
| --- | --- |
| **ETW zeigt 0 Ereignisse / 0 Bandbreite** | Tatsächlichen Netzwerkverkehr erzeugen; prüfen, ob weitere Instanzen laufen; **ETW neu starten**; Berechtigungen und Windows-ETW-Sitzungszustand prüfen. |
| **Browser-Tabs fehlen** | Erweiterung installiert/aktiv? Pairing-Code richtig? Browser und THES4INTWIRE laufen? Listener-Port `127.0.0.1:38471` frei? |
| **Tab-Traffic zeigt —** | Berechtigungen der neuen Erweiterung prüfen; Tab neu laden; Debugger möglicherweise durch andere DevTools-Sitzung belegt; Browser-Unterstützung beachten. |
| **Firefox-Erweiterung verschwunden** | Temporäre Erweiterung nach Browser-Neustart erneut laden. |
| **PTR gibt NXDOMAIN/NO_RECORDS aus** | Nicht jede IP hat einen PTR-Eintrag; bei Bedarf später erneut prüfen. |
| **RDAP zeigt keinen Betreiber** | Abfrage kann scheitern oder Daten können unvollständig sein; PTR und RDAP nicht mit tatsächlicher Website gleichsetzen. |
| **„Jetzt analysieren“ ändert nichts** | Lokaler IOC-Abgleich findet möglicherweise keinen Treffer; **Online-Reputation prüfen** ist eine separate Aktion. |
| **VirusTotal/AbuseIPDB ohne Ergebnis** | API-Schlüssel, Rate-Limit, Konnektivität und Anzahl bereits geprüfter IPs kontrollieren. |
| **GitHub bietet „Source code“ an** | Automatische Archive des öffentlichen GitHub-Repositories. Die Windows-EXE aus dem **eigenen Release-Asset** laden. |

## 10. Glossar

| Begriff | Bedeutung |
| --- | --- |
| **API** | Programmierschnittstelle für einen Dienst |
| **ASN** | Nummer eines autonomen Netzes im Internet |
| **CDP** | Chrome DevTools Protocol – Browser-Diagnoseschnittstelle |
| **CIDR** | Schreibweise für IP-Adressbereiche, z. B. `192.0.2.0/24` |
| **ETW** | Event Tracing for Windows – Windows-Ereigniserfassung |
| **IOC** | Indicator of Compromise – ein möglicherweise relevanter Sicherheitsindikator |
| **IP** | Internet-Protocol-Adresse |
| **PID** | Windows-Prozess-ID |
| **PTR** | DNS-Eintrag zur Rückwärtsauflösung einer IP-Adresse |
| **RDAP** | Registration Data Access Protocol – Registrierungsdaten eines IP-Netzes |
| **RX / TX** | Receive (Empfang) / Transmit (Senden) |
| **TCP / UDP** | Netzwerktransportprotokolle |
| **TLS** | Transportverschlüsselung, unter anderem für HTTPS |
| **Threat Intelligence** | Kontext- und Reputationsinformationen über mögliche Bedrohungen |
| **VirusTotal** | Dienst zur Sammlung und Auswertung von Sicherheitsbewertungen |
| **AbuseIPDB** | Dienst für Meldungen über potenziellen Missbrauch von IP-Adressen |

---

### Dokumentation, Support und Sicherheit

- [Projektübersicht](README.md)
- [Browser-Bridge-Setup](docs/BROWSER-SETUP-DE.md)
- [Tab-Traffic-Messgrenzen](docs/TAB-TRAFFIC-DE.md)
- [Lokale Threat Intelligence](docs/THREAT-INTELLIGENCE-DE.md)
- [Online-Reputation](docs/REPUTATION-SETUP-DE.md)
- [Changelog](CHANGELOG.md)
- [Fehler melden](../../issues)
- [Sicherheitsrichtlinie](SECURITY.md)

**Hinweis für Fehlermeldungen:** Keine privaten IP-Inventare, API-Schlüssel, persönlichen Browser-URLs oder Benutzernamen in öffentliche GitHub-Issues kopieren.

**© 2026 TheS4int · Proprietary Freeware · Closed Source**
