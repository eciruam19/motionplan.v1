# DFFB Motionplan Deployment-Anleitung

Diese Anleitung beschreibt den Prozess zum Deployment des DFFB Motionplan-Systems auf Cloudflare Pages.

## Voraussetzungen

- Cloudflare-Konto
- GitHub-Konto
- Git auf dem lokalen System installiert
- Node.js und npm auf dem lokalen System installiert

## Schritt 1: Repository auf GitHub erstellen

1. Melden Sie sich bei GitHub an
2. Erstellen Sie ein neues Repository (z.B. "dffb-motionplan")
3. Folgen Sie den Anweisungen, um das lokale Repository zu initialisieren und hochzuladen:

```bash
cd /home/ubuntu/dffb-motionplan-implementation
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/IhrUsername/dffb-motionplan.git
git push -u origin main
```

## Schritt 2: Cloudflare Pages konfigurieren

1. Melden Sie sich bei Cloudflare an
2. Navigieren Sie zu "Pages"
3. Klicken Sie auf "Create a project"
4. Wählen Sie "Connect to Git"
5. Autorisieren Sie Cloudflare, auf Ihre GitHub-Repositories zuzugreifen
6. Wählen Sie das "dffb-motionplan" Repository aus
7. Konfigurieren Sie das Projekt:
   - **Project name**: dffb-motionplan
   - **Production branch**: main
   - **Build settings**:
     - **Framework preset**: Next.js
     - **Build command**: npm run build
     - **Build output directory**: .next
   - **Environment variables**:
     - `NODE_VERSION`: 18.x
     - `NEXTAUTH_URL`: https://dffb-motionplan.pages.dev (oder Ihre benutzerdefinierte Domain)
     - `NEXTAUTH_SECRET`: [Generieren Sie einen sicheren Schlüssel]

8. Klicken Sie auf "Save and Deploy"

## Schritt 3: Datenbank konfigurieren

1. Navigieren Sie in Ihrem Cloudflare-Dashboard zu "Workers & Pages"
2. Wählen Sie Ihr dffb-motionplan-Projekt
3. Gehen Sie zu "Settings" > "Functions"
4. Unter "D1 Database Bindings", klicken Sie auf "Add binding"
5. Erstellen Sie eine neue D1-Datenbank oder wählen Sie eine bestehende aus
6. Setzen Sie den Variablennamen auf `DB` (wie in wrangler.toml definiert)
7. Speichern Sie die Einstellungen

## Schritt 4: Datenbank-Migrationen ausführen

1. Installieren Sie die Wrangler CLI, falls noch nicht geschehen:
   ```bash
   npm install -g wrangler
   ```

2. Authentifizieren Sie sich bei Cloudflare:
   ```bash
   wrangler login
   ```

3. Führen Sie die Migrationen aus:
   ```bash
   wrangler d1 migrations apply DB --production
   ```

## Schritt 5: R2 Storage für Dokumente konfigurieren

1. Navigieren Sie in Ihrem Cloudflare-Dashboard zu "R2"
2. Erstellen Sie einen neuen Bucket (z.B. "dffb-motionplan-documents")
3. Gehen Sie zurück zu Ihrem Pages-Projekt
4. Unter "Settings" > "Functions" > "R2 Bucket Bindings", klicken Sie auf "Add binding"
5. Wählen Sie Ihren erstellten Bucket aus
6. Setzen Sie den Variablennamen auf `DOCUMENTS` (wie im Code definiert)
7. Speichern Sie die Einstellungen

## Schritt 6: Benutzerdefinierte Domain konfigurieren (optional)

1. Navigieren Sie zu Ihrem Pages-Projekt
2. Gehen Sie zu "Settings" > "Custom domains"
3. Klicken Sie auf "Set up a custom domain"
4. Folgen Sie den Anweisungen, um Ihre Domain zu konfigurieren
5. Aktualisieren Sie die `NEXTAUTH_URL` Umgebungsvariable, um Ihre benutzerdefinierte Domain zu verwenden

## Schritt 7: Ersten Administrator-Benutzer erstellen

Nach dem ersten Deployment müssen Sie einen Administrator-Benutzer erstellen:

1. Besuchen Sie Ihre Anwendung (https://dffb-motionplan.pages.dev oder Ihre benutzerdefinierte Domain)
2. Gehen Sie zur Registrierungsseite (/register)
3. Erstellen Sie einen neuen Benutzer
4. Verwenden Sie die Cloudflare D1-Konsole, um die Rolle des Benutzers auf "admin" zu setzen:
   ```sql
   UPDATE users SET role = 'admin' WHERE email = 'ihre-email@beispiel.de';
   ```

## Fehlerbehebung

### Problem: Build-Fehler
- Überprüfen Sie die Build-Logs in Cloudflare Pages
- Stellen Sie sicher, dass alle Abhängigkeiten korrekt installiert sind
- Überprüfen Sie die Node.js-Version

### Problem: Authentifizierungsfehler
- Stellen Sie sicher, dass `NEXTAUTH_URL` und `NEXTAUTH_SECRET` korrekt gesetzt sind
- Überprüfen Sie, ob die Datenbank korrekt konfiguriert ist

### Problem: Datei-Upload funktioniert nicht
- Überprüfen Sie die R2-Bucket-Konfiguration
- Stellen Sie sicher, dass die entsprechenden Berechtigungen gesetzt sind

## Wartung und Updates

Um das System zu aktualisieren:

1. Nehmen Sie Änderungen am lokalen Code vor
2. Committen und pushen Sie die Änderungen zu GitHub:
   ```bash
   git add .
   git commit -m "Update: Beschreibung der Änderungen"
   git push
   ```
3. Cloudflare Pages wird automatisch ein neues Deployment starten

## Sicherheitshinweise

- Ändern Sie regelmäßig das `NEXTAUTH_SECRET`
- Überwachen Sie die Zugriffslogs
- Führen Sie regelmäßige Backups der Datenbank durch
- Halten Sie alle Abhängigkeiten aktuell

## Support

Bei Fragen oder Problemen wenden Sie sich bitte an den Support unter [support@beispiel.de].
