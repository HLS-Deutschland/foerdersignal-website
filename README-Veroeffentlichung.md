# Veröffentlichung der Website – Stand 16.09.2026, 18:25 Uhr

**Erledigt:** Repository `HLS-Deutschland/foerdersignal-website` (main) und Netlify-Projekt `foerdersignal` → **https://foerdersignal.netlify.app**
(per Upload deployt, Formular live getestet). Schritte 1–3 unten sind damit durch. **Offen: Schritt 4 (Domain) und Schritt 5 (Brevo)**, plus
einmalig: Netlify-GitHub-App für das neue Repo freischalten (github.com/settings/installations → Netlify → Repository access → foerdersignal-website),
damit künftige Änderungen automatisch aus `main` deployen. Bis dahin: Änderungen als Upload unter app.netlify.com/projects/foerdersignal/deploys.

---

## Ursprüngliche Schrittliste

Ins Repository gehören genau diese vier Dateien aus `03_Auftritt/`: `index.html`, `musterausgabe.html`, `netlify.toml`, `README-Veroeffentlichung.md`.
Nicht hochladen: `index_v1_2026-09-15.html.bak`, `DNS-Eintraege_foerdersignal.de.md`.

1. **GitHub:** In der Organisation `HLS-Deutschland` ein neues Repository `foerdersignal-website` anlegen (privat oder öffentlich, beides geht).
   Über „Add file → Upload files" die vier Dateien hochladen, Commit „Website v2, 16.09.2026".
2. **Netlify:** Im Team `gpgeschwinder` → „Add new site → Import an existing project → GitHub" → Repository `foerdersignal-website` wählen.
   Build command leer lassen, Publish directory `.` (Punkt). Deploy.
3. **Test auf der Netlify-Adresse** (`irgendwas.netlify.app`): Seite öffnen, Formular mit einer eigenen Adresse ausfüllen, absenden.
   Erwartung: grüne Meldung „Danke. Bitte bestätigen Sie …". Die Bestätigungsmail liegt dann in `funding.outbox` (noch kein automatischer Versand).
4. **Domain:** Netlify → Domain management → `foerdersignal.de` und `fördersignal.de` hinzufügen. Netlify zeigt die DNS-Werte an.
   Bei GoDaddy eintragen: A-Record `@` → Netlify-Load-Balancer-IP, CNAME `www` → Netlify-Adresse. Die vorhandenen MX/SPF/DKIM/DMARC-Einträge
   für `foerdersignal.de` **nicht anfassen** (Mail läuft darüber). HTTPS aktiviert Netlify automatisch (Let's Encrypt).
5. **Brevo:** Konto anlegen, Domain `foerdersignal.de` verifizieren (DKIM ist bereits gesetzt, SPF enthält Brevo). API-Schlüssel an die Code-Sitzung
   geben – nur in den Supabase-Vault, nie in eine Datei. Danach baut die Code-Sitzung den Versandschritt aus der Outbox und du gibst ihn frei.

Bis Schritt 5 gilt: Bestätigungsmails aus `funding.outbox` werden von Hand von `report@foerdersignal.de` verschickt (Text steht in der Zeile).
