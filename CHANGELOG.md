# CHANGELOG – apimeetsai.com

## [2.0.0] – 2026-05-09

### Neue Module

#### `/api/autobahn` – Bundesautobahnen (AutobahnModule.php)
- Quelle: Autobahn GmbH des Bundes (`verkehr.autobahn.de`), vollständig keyless
- Baustellen, Verkehrswarnungen, Sperrungen, Rastplätze, Webcams für alle Bundesautobahnen
- Parameter: `?aktion=liste|baustellen|warnungen|sperrungen|rastplaetze|webcams&strasse=A1`

#### `/api/blaulicht` – Polizei & Feuerwehr (BlaulichtModule.php)
- Quelle: Presseportal.de RSS-Feeds (`dienststelle_{ID}.rss2`), keyless
- **48 verifizierte NRW-Dienststellen** mit echten Feed-IDs (35 Polizei, 13 Feuerwehr)
 – alle IDs live gegen die RSS2-Feeds geprüft (Mai 2026)
- Polizeipräsidien NRW u.a.: Köln (12415), Düsseldorf (13248), Dortmund (4971),
 Essen (11562), Bonn (7304), Bochum (11530), Aachen (11559), Münster (11187),
 Duisburg (50510), Wuppertal (11811)
- NRW-Kreisbehörden: ID-Range 65841–65858 vollständig (Euskirchen bis Wesel)
- NRW-Feuerwehren: ID-Range 115868–115891 (Bochum, Dortmund, Düsseldorf, Köln u.v.m.)
- Weitere Bundesländer: Hamburg, Hessen, Rheinland-Pfalz, Niedersachsen, Thüringen u.a.
- Filter: `?region=nrw`, `?typ=polizei|feuerwehr`, `?dienststelle=ID`, `?suche=Unfall`
- Recherche-Methode: Dienststellen-IDs über `presseportal.de/suche/Polizei/blaulicht`
 und systematischen Scan der ID-Ranges ermittelt

#### `/api/events` – Veranstaltungskalender (EventsModule.php)
- Quelle: Stadt Köln Open Data (`stadt-koeln.de`, CC BY), keyless
- Aktuelle Veranstaltungen mit Stadtbezirk, Koordinaten, Kategorie, ÖPNV-Info
- Filter: `?ndays=`, `?suche=`, `?stadtbezirk=`, `?kategorie=`
- Kategorien-Endpoint: `?aktion=kategorien` (63 Kategorien live abgerufen)
- Städteübersicht: `?aktion=staedte` (Status weiterer geplanter Quellen)
- Hinweis auf `/api/wikipedia?aktion=heute` für historische Ereignisse
- Recherche-Ergebnis: Andere deutsche Städte (Berlin, Wien, München) bieten
 derzeit keine stabilen keyless JSON-APIs für Veranstaltungen

### Erweiterte Module

#### `/api/politik` – Erweiterung um DAWUM + DIP (PolitikModule.php)
Bisherige Abgeordnetenwatch-Funktionen bleiben vollständig erhalten, nun unter `?quelle=aw`.
Neues Routing: Erster Aufruf ohne `quelle=` zeigt Übersicht aller drei Quellen.

**Neu: DAWUM – Wahlumfragen (`?quelle=dawum`)**
- Quelle: `api.dawum.de/newest_surveys.json`, ODbL-Lizenz
- Neueste Wahlumfragen für Bundestag und alle 16 Landtage + Europaparlament
- 18 Parlamente (ID 0–17), alle Institute und Parteien aufgeschlüsselt
- Ergebnisse sortiert nach Prozentwert, mit Institut und Auftraggeber
- Fix: User-Agent-Header nötig (`apimeetsai.com/1.0`) da DAWUM sonst blockiert

**Neu: DIP Bundestag (`?quelle=dip`)**
- Quelle: `search.dip.bundestag.de/api/v1`, öffentlicher Key `OSOegLs.PR2lwJ1dwCeje9vTj7FPOt3hvpYKkhw`
- Vorgänge/Gesetzgebung (`?aktion=vorgaenge`): Volltextsuche, Wahlperiode-Filter
- Drucksachen (`?aktion=drucksachen`): aktuelle parlamentarische Dokumente
- MdB-Suche (`?aktion=mdb`): alle Abgeordneten, filterbar nach Name und Wahlperiode
- Paginierung über `?seite=` bei allen Endpunkten

### Abgelehnte Kandidaten (nach Live-Prüfung)

| Kandidat | Ergebnis | Begründung |
|---|---|---|
| OParl (Ratsinfosysteme) | Abgelehnt | Überwiegend defekt oder 404, keine verlässliche Quelle |
| Presseportal JSON-API | Kein Key | Strukturierte API erfordert eigenen API-Key |
| Destatis GENESIS | Registrierung | Erfordert kostenlosen Account + Passwort |
| DZT Tourismus-API | Kein Key | API-Key per E-Mail erforderlich |
| Kulturdaten Berlin | Instabil | Lesezugriff ohne Auth noch nicht produktionsreif |
| Wien Events | Instabil | Keine stabile JSON-API keyless verfügbar |
| NRW Tourismus et4 | Blockiert | 401 / keine öffentliche API |

### Korrekturen & Verbesserungen

- **PolitikModule**: Alte Abgeordnetenwatch-Routen auf `?quelle=aw` umgestellt;
 `?aktion=politiker` war vorher direkt, ist jetzt `?quelle=aw&aktion=politiker`
- **SystemModule**: Modulbeschreibungen für alle neuen Module ergänzt;
 Next-Steps um Autobahn, Blaulicht, Events und die erweiterte Politik-Navigation erweitert
- **index.php**: Neue Tabelle „Verfügbare Module & Aktionen" als Schnellübersicht
 in der HTML-Ansicht für Browser-Nutzer eingefügt (vor dem Skill-Bereich)
- **SKILL.md**: Vollständig neu geschrieben (v2.0.0), alle neuen Endpunkte dokumentiert
- **AGENTS.md**: Modulbeschreibungen für alle neuen Endpunkte ergänzt,
 externe APIs-Liste aktualisiert

---

## [1.0.0] – 2026 (Erstveröffentlichung)

### Initiale Module
- `/api/wetter` – Open-Meteo (Wetter + 7-Tage-Vorhersage, keyless)
- `/api/dwd` – Deutscher Wetterdienst (Lageberichte + Warnungen, keyless)
- `/api/sport` – OpenLigaDB (Bundesliga, DFB, CL/EL, keyless)
- `/api/pegel` – Pegelonline WSV (Echtzeit-Pegelstände, keyless)
- `/api/waehrungen` – EZB via Frankfurter API (Wechselkurse, keyless)
- `/api/krypto` – CoinGecko (Top-20 Kryptos, keyless)
- `/api/wikipedia` – Wikimedia REST API (Artikel, Suche, OnThisDay, keyless)
- `/api/politik` – Abgeordnetenwatch (Politikerprofile + Abstimmungen, CC0, keyless)
- `/api/geo` – OpenStreetMap / Overpass + Nominatim (POI, keyless)
- `/api/news` – RSS-Aggregator (BBC, Reuters, DW, Spiegel u.a., keyless)
- `/api/legal` – Impressum & Datenschutz
- Rate-Limiting: 50 Anfragen/Minute/IP
- Bot-Advertising: sponsored-Block mit strikter Trennung vom payload
- Mehrsprachigkeit: DE, EN, FR, ES, ZH, RU via Lang.php
- HTML-Fallback für Browser, JSON für Maschinen (Accept-Header-Erkennung)
