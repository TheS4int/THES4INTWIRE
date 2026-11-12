# THES4INTWIRE v1.21 – Browser Intelligence einrichten

**Unterstützt:** Google Chrome, Brave, Opera, Microsoft Edge und Firefox.
**Tor:** Netzverbindungen bleiben sichtbar, Tor-Tabs werden nicht ausgelesen (Schutz der Anonymität).

## Lokale Kopplung (einmal je Browser)

1. THES4INTWIRE starten, **Prozesse & Verbindungen** öffnen und auf **Pairing-Code anzeigen** klicken.
2. Chromium-Browser (Chrome, Brave, Opera, Edge): in die Erweiterungsverwaltung (`chrome://extensions`, `brave://extensions`, `opera://extensions` bzw. `edge://extensions`) wechseln, Entwicklermodus einschalten, **Entpackte Erweiterung laden** auswählen und den Ordner `browser-extensions/chromium` wählen.
3. Firefox: `about:debugging#/runtime/this-firefox` öffnen, **Temporäres Add-on laden** wählen und `browser-extensions/firefox/manifest.json` auswählen. Temporäre Add-ons bleiben nicht über einen Neustart erhalten; für eine dauerhafte Installation muss eine signierte Erweiterung veröffentlicht werden.
4. Im Erweiterungsfenster deinen Browser auswählen, Pairing-Code eintragen und speichern. Danach aktualisiert sich die lokale Tab-Anzeige automatisch bei Tabwechseln und regelmäßig.

**Einmalige Berechtigung:** Browser verlangen die ausdrückliche Erlaubnis beim Installieren der Erweiterung. Es gibt keine Abfrage bei jedem Tababruf. Unternehmenseinstellungen können Erweiterungen blockieren; nicht umgehen.

## Datenschutz / Grenzen

- Die Erweiterung sieht nur normale Browserfenster, nicht Inkognito-/private Fenster.
- Es werden Tabtitel und URL **ohne Query-Parameter und Fragmente** verarbeitet; keine Cookies, Passwörter oder Seiteninhalte.
- Die Daten gelangen nur zur lokalen Anwendung auf `127.0.0.1:38471`; der Pairing-Code ist erforderlich. Keine externe Cloud.
- Daten werden ausschließlich im Arbeitsspeicher gehalten und nach 90 Sekunden ohne neue Übertragung ausgeblendet.
- **Die Tab-Liste weist nicht nach, welcher Browser-Tab eine bestimmte TCP/IP-Verbindung verursacht hat.**
- Die Browser-Erweiterung ist **nicht** Bestandteil der Windows-EXE; sie muss je Browser eingerichtet werden.
- Wenn die Browser Bridge als nicht gestartet erscheint, wird der lokale Port vermutlich bereits von einer anderen Anwendung belegt.
