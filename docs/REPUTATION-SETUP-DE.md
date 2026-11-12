# THES4INTWIRE v1.24 – Online Reputation

1. Unter **Threat Intelligence** mindestens einen API-Schlüssel eintragen (VirusTotal bzw. AbuseIPDB). Die Schlüssel bleiben nur im laufenden App-Fenster und werden nicht dauerhaft gespeichert.
2. **Lokal analysieren** aktualisiert die Netzwerkverbindungen und lokale IOC-Liste, ohne IPs an Reputationsdienste zu übertragen.
3. **Online-Reputation prüfen** fragt höchstens drei unterschiedliche öffentliche IP-Adressen pro Klick ab. Die Reihenfolge folgt der aktuell erfassten Verbindungsliste, nicht einer Gefährlichkeitsbewertung.
4. Ergebnisse zeigen getrennte VT-malicious/suspicious-Werte, AbuseIPDB-Confidence/Reports, Zeitpunkt und die abgeleitete Priorität.
5. Mehrfachabfragen für bereits erfolgreich geprüfte IPs werden übersprungen. Bei Fehlern kann die Auswahl **Nur noch nicht online geprüfte IPs** deaktiviert werden, um erneut zu versuchen.
6. **Kein Hinweis** heißt *nicht sicher*, sondern lediglich kein Hinweis gemäß den gewählten Schwellenwerten in verfügbaren Berichten.

## Hinweis-Index
Der angezeigte Hinweis-Index (0–100) ist eine **frei definierte Priorisierungsheuristik**, keine Wahrscheinlichkeit einer Infektion: lokal bestätigte IOC-Übereinstimmung = 100, andernfalls Maximum aus `min(100, 20 × VT malicious + 8 × VT suspicious)` und `AbuseIPDB Confidence`. Ohne Anbieterbericht und IOC-Treffer zeigt die App `—`.

## Bewertungsregel
- Lokale IOC-Übereinstimmung: `IOC-TREFFER`, unabhängig von Online-Quellen.
- `HOHER HINWEIS`: mindestens 3 VT-malicious-Meldungen oder AbuseIPDB-Confidence ≥80.
- `PRÜFEN`: mindestens eine VT-malicious/suspicious-Meldung oder AbuseIPDB-Confidence ≥25.
- `KEIN HINWEIS`: mindestens ein Anbieter hat Daten geliefert, Schwellenwerte wurden nicht überschritten.
- `NICHT BEWERTET`: keine verwertbaren Berichte.

**Achtung:** Die Priorität ist eine dokumentierte Heuristik und keine Wahrscheinlichkeit oder bestätigte Malware-Diagnose.

## Datenschutz und Limits
Die Abfrage gibt die IP an den jeweiligen Drittanbieter weiter. VirusTotal kann abgefragte Indikatoren seiner Datenbasis hinzufügen. Keine vertraulichen IPs/Umgebungsdaten senden. Die öffentliche VT-API hat enge Limits (typischerweise vier Anfragen pro Minute) und Nutzungsbedingungen; der Nutzer muss diese selbst beachten. Keine automatischen periodischen Online-Abfragen.

Offizielle APIs:
- https://docs.virustotal.com/reference/ip-info
- https://www.abuseipdb.com/api.html (API v2 check)

Die bisherige ETW-Implementierung, Browser Intelligence und lokale Watchlist wurden nicht verändert.
