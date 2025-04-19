# DFFB Motionplan

DFFB Motionplan ist ein umfassendes Projektverwaltungssystem für die Deutsche Film- und Fernsehakademie Berlin (DFFB). Das System ermöglicht die digitale Abbildung des gesamten Prozesses von der Projektanmeldung über die Produktion bis zur Postproduktion und Abrechnung.

## Funktionen

- **Projektverwaltung**: Anmeldung, Freigabe und Monitoring von Projekten
- **Vertragsverwaltung**: Erstellung und Verwaltung von Vertragsvorlagen und Verträgen
- **Dokumentenmanagement**: Upload, Versionierung und Verwaltung von Projektdokumenten
- **V-Geld-Verarbeitung**: Anträge, Genehmigungen und Abrechnungen
- **Admin-Bereich**: Benutzerverwaltung, Vorlagenverwaltung und Systemeinstellungen
- **Rollenbasierte Berechtigungen**: Unterschiedliche Zugriffsrechte für Studenten, Dozenten, Produktion, Direktion und Administratoren

## Technologie-Stack

- **Frontend**: Next.js, React, Tailwind CSS
- **Backend**: Next.js API Routes, Cloudflare Workers
- **Datenbank**: Cloudflare D1 (SQLite-kompatibel)
- **Speicher**: Cloudflare R2 für Dokumente und Dateien
- **Authentifizierung**: NextAuth.js
- **Deployment**: Cloudflare Pages

## Erste Schritte

### Installation

1. Repository klonen:
   ```bash
   git clone https://github.com/IhrUsername/dffb-motionplan.git
   cd dffb-motionplan
   ```

2. Abhängigkeiten installieren:
   ```bash
   npm install
   ```

3. Umgebungsvariablen konfigurieren:
   Erstellen Sie eine `.env.local` Datei mit den folgenden Variablen:
   ```
   NEXTAUTH_URL=http://localhost:3000
   NEXTAUTH_SECRET=IhrGeheimesToken
   ```

4. Entwicklungsserver starten:
   ```bash
   npm run dev
   ```

5. Öffnen Sie [http://localhost:3000](http://localhost:3000) im Browser.

### Deployment

Für Anweisungen zum Deployment des Systems auf Cloudflare Pages, lesen Sie bitte die [Deployment-Anleitung](deployment.md).

## Projektstruktur

- `/src/app`: Next.js App Router Seiten und API-Routen
- `/src/components`: React-Komponenten
- `/src/lib`: Hilfsfunktionen und Utilities
- `/src/styles`: CSS und Styling
- `/public`: Statische Assets
- `/migrations`: Datenbankmigrationen

## Entwicklung

### Tests ausführen

```bash
npm run test
```

### Code-Formatierung

```bash
npm run lint
npm run format
```

## Dokumentation

- [Datenbankschema](database_schema.md)
- [Systemarchitektur](system_architecture.md)
- [API-Dokumentation](api_documentation.md)
- [Benutzerhandbuch](user_guide.md)

## Support

Bei Fragen oder Problemen wenden Sie sich bitte an den Support unter [support@beispiel.de].

## Lizenz

Dieses Projekt ist urheberrechtlich geschützt und darf nur mit ausdrücklicher Genehmigung der DFFB verwendet werden.
