# Migration from local HomeHeat apps

Persistent HomeHeat data lives in `/share/homeheat` and is shared between app installations.

1. Add this repository to Home Assistant.
2. Install the repository copies of all three apps, but do not start them yet.
3. Copy the options/credentials from the existing local apps.
4. Stop the old local apps.
5. Start, in order:
   1. HomeHeat Logger
   2. Naturela MQTT Bridge
   3. HomeHeat Model
6. Verify MQTT entities, `/share/homeheat/homeheat.sqlite`, model status, forecast sensors and calendars.
7. Uninstall the old local copies only after verification.

Do not run the old and repository-backed Logger or Naturela MQTT Bridge simultaneously; that would duplicate logging and MQTT publication.

The HomeHeat Model remains proposal-only: it writes to the Test Heating Plan, never the live Heating Plan.
