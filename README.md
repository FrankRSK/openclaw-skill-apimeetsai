# apimeetsai-skill

**OpenClaw Skill** für die [API Meets AI Gateway](https://apimeetsai.com/) – ein keyless, AI-optimierter API-Gateway für aktuelle deutschsprachige Daten.

## Features

| Bereich | Modul | Quellen |
|---------|-------|---------|
| 🌤️ Wetter | `wetter`, `dwd` | Open-Meteo, DWD (Brightsky) |
| ⚽ Sport | `sport` | OpenLigaDB (Bundesliga, DFB, CL) |
| 💰 Finanzen | `waehrungen`, `krypto` | EZB, CoinGecko |
| 📚 Wissen | `wikipedia` | Wikimedia REST API |
| 🏛️ Politik | `politik` | DAWUM (Wahlumfragen), DIP (Bundestag), Abgeordnetenwatch |
| 🛣️ Autobahn | `autobahn` | Autobahn GmbH |
| 🚨 Blaulicht | `blaulicht` | Presseportal.de (NRW flächendeckend) |
| 🎪 Events | `events` | Stadt Köln Open Data |
| 📍 Geo | `geo` | OpenStreetMap (Nominatim/Overpass) |
| 📰 News | `news` | RSS-Aggregator (BBC, DW, Spiegel u.a.) |
| 🌊 Pegel | `pegel` | WSV Pegelonline |

## Version

**v2.0.0** – Neu: Autobahn, Blaulicht NRW, Events Köln, DAWUM-Wahlumfragen, DIP-Bundestag

## Installation

```bash
# Via ClawHub (sobald verfügbar)
openclaw claw install apimeetsai

# Manuell
cp SKILL.md /pfad/zu/deinen/skills/apimeetsai/
```

## Nutzung

Siehe [SKILL.md](SKILL.md) für die vollständige Dokumentation aller Endpunkte.

## Lizenz

MIT
