# Threat Intelligence Center – v1.22

## Umfang

Das neue Menü **Threat Intelligence** korreliert laufende ausgehende Prozessverbindungen mit einer lokal gespeicherten IOC-Liste. Unterstützt IPv4-Einzeladressen, IPv4-CIDR-Netze und IPv6-Einzeladressen. Kein Treffer bedeutet ausdrücklich nicht sicher.

## Bedienung

1. Menü Threat Intelligence öffnen.
2. IOCs zeilenweise eintragen: `1.2.3.4 | Fallnummer / Beschreibung` oder `1.2.3.0/24 | Notiz`.
3. **IOC-Liste speichern** klicken. Die Liste wird lokal im WebView-Speicher gespeichert, nicht synchronisiert.
4. Tabelle filterbar nach Treffern, Prozess, PID, IP und Port.
5. PTR und RDAP erfolgen nur per Klick und können DNS-/RDAP-Anfragen nach außen auslösen.

**Wichtig:** Testnetzadressen (`203.0.113.0/24`) erscheinen nicht in der Tabelle der öffentlichen Ziele. Zum Funktionstest kann eine bekannte, selbst kontrollierte öffentliche Test-IP eingetragen werden; keine fremden IPs als bösartig deklarieren.

## Einordnung

Der lokale IOC-Abgleich ist eine funktionierende Analysegrundlage, **keine automatische Online-Reputationsdatenbank**. Es werden keine Prozesse blockiert. Die alte Windows-ETW-Erfassung und Browser Bridge wurden nicht verändert. Ungenauigkeiten von Betriebssystem-Endpunktlisten bleiben möglich. Die App wurde nicht unter Windows validiert.
