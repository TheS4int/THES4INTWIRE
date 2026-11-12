# THES4INTWIRE v1.23 – Tab Traffic in Browser Intelligence

## Neue Tabelle

Die bisherige Browser-Intelligence-Tabelle enthält jetzt **↓ Download** und **↑ Upload** zwischen Website und Aktiv. Angezeigt wird jeweils die zuletzt gemessene Rate (pro Sekunde) und die kumulierte, browserseitig beobachtete Datenmenge seit dem Start der Erfassung bzw. Domainwechsel. Bei Platzmangel ist die Tabelle horizontal scrollbar, ohne bisherige Spalten zu entfernen.

## Chromium: Chrome, Brave, Opera und Edge

Die Erweiterung benötigt jetzt die Berechtigung **debugger**. Nach Neuinstallation/Neuladen und bestehendem Pairing-Code wird sie sich an normale Webseiten-Tabs anschließen und CDP-Network-Ereignisse zählen. **Das Betriebssystem bzw. der Browser kann eine sichtbare Meldung anzeigen, dass der Tab durch eine Erweiterung debuggt wird. Diese Warnung lässt sich nicht seriös umgehen.** Bei einer schon aktiven DevTools-Sitzung, inkompatiblen Browser-Versionen oder nicht erlaubter Debugger-Nutzung werden keine Werte gezeigt (—), statt Werte zu erfinden.

↓ Download: `Network.dataReceived.encodedDataLength`, beim Abschluss mit `Network.loadingFinished.encodedDataLength` abgeglichen. Das sind erfasste Browser-Netzwerk-Bytes je Anfrage, **keine vollständigen Leitungspakete einschließlich Overhead**.

↑ Upload: nur beobachtete HTTP-Request-Bodies aus CDP `request.postData`, **nicht** sämtlicher gesendeter TCP-/TLS-Verkehr, WebSockets oder Browserprotokoll-Overhead. Die App zeigt nur Zähler an; Request-Inhalte werden nicht übermittelt oder gespeichert. Eine angezeigte 0 kann bedeuten, dass die Bytes durch diese Quelle nicht beobachtbar waren.

## Firefox

Firefox nutzt `webRequest.filterResponseData`: eingehende HTTP-Antwortkörper werden byteweise gezählt und **unverändert weitergereicht**. Dazu benötigt die Erweiterung `webRequest`, `webRequestBlocking`, `webRequestFilterResponse` sowie Webzugriff (`<all_urls>`). **Keine Netzpaket-/Kompressions-Bytezählung**; nicht alle Browser-Netzwerkbytes sind enthalten. Upload wird als — (nicht verfügbar) angezeigt.

## Einrichtung / Aktualisierung

1. THES4INTWIRE v1.23 starten (Pairing-Code bleibt bei unverändertem Windows-Profil bestehen).
2. In Chrome/Brave/Opera/Edge `...://extensions` aufrufen, die alte THES4INTWIRE-Erweiterung entfernen und den Ordner `browser-extensions/chromium` erneut als entpackte Erweiterung laden. Dabei neue **debugger**-Berechtigung bestätigen.
3. Firefox: Unter `about:debugging#/runtime/this-firefox` die alte temporäre Erweiterung entfernen und `browser-extensions/firefox/manifest.json` neu laden. Die erforderlichen Berechtigungen bestätigen. Temporäre Firefox-Add-ons überstehen keinen Browser-Neustart.
4. Falls das Pairing durch Neuinstallation verloren ging, in Browser Intelligence den Pairing-Code anzeigen und in den Optionen der Browsererweiterung erneut speichern.
5. Eine Webseite neu laden bzw. Netzwerkverkehr erzeugen. Die Tab-Raten aktualisieren sich ereignisbasiert, die App-Tabelle etwa alle drei Sekunden.

**Datenschutz:** Der Listener verarbeitet nur normale Browser-Tabs. Keine privaten Fenster und kein Tor Browser. Tab-Titel und URL ohne Parameter/Fragment sowie numerische Traffic-Zähler gehen ausschließlich an den lokal laufenden HTTP-Dienst auf `127.0.0.1:38471`. Der Pairing-Code bleibt erforderlich. Keine DNS-/Reputations-Uploads durch diese Funktion.

**Wichtig:** ETW-Prozessraten und Browser-Tabraten haben unterschiedliche Messpunkte. Sie dürfen weder eins-zu-eins gleichgesetzt noch einfach addiert werden. Die bestehende ETW-Implementierung wurde nicht verändert.

**Teststand:** JavaScript-Syntax, JSON-Manifest und ZIP-Paket validiert. Der Windows-Build und das Verhalten realer Browser konnten hier nicht ausgeführt werden.
