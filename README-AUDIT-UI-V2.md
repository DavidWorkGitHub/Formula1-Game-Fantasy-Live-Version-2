# F1 25 Fantasy Live — Audit + UI v2

## What was checked

- Node syntax for `server.js`, `data-manager.js`, `weekend-manager.js`, `simulate.js`.
- Browser-side JavaScript syntax from `index.html`.
- Automatic weekend state-machine progression.
- UDP packet parsing using the included simulator.
- Persistence across a full process restart.
- Dashboard HTTP serving.
- Sprint Qualifying scoring and weekend totals.
- Season-history aggregation.
- F1 25 / 2026 Season Pack track-ID mapping.

## Fixes in this build

1. **Dashboard 404 fixed** — the app now serves the bundled `index.html` from the project root.
2. **Track IDs fixed** — UDP track IDs are mapped to the championship calendar instead of assuming `trackId + 1` is the round.
3. **Sprint Qualifying scoring fixed** — SQ now contributes its qualifying-style points to the weekend total and constructor totals.
4. **History aggregation fixed** — a qualifying result no longer gets overwritten by the later race result. History now stores the cumulative weekend total for the round.
5. **Persistence improved** — the weekend manager's locked/completed/waiting/complete state is restored after restart.
6. **Duplicate/replay protection retained** — locked sessions remain immutable.
7. **Empty-table column counts fixed** for standard and sprint views.
8. **Setup page now displays the actual UDP port from the server state.**
9. **UI refreshed** — full-width driver/constructor sections, cleaner hierarchy, collapsible history drawer, clearer session flow, improved mobile layout, and less developer-looking controls.

## Weekend flow

### Standard weekend
`Qualifying → Race`

### Sprint weekend
`Sprint Qualifying → Sprint → Qualifying → Race`

Practice is ignored. Once a scoring phase is locked, later telemetry cannot overwrite it.

## Data location

Persistent data remains outside the project folder by default:

`Documents/F1 Fantasy Live/`

This means replacing the project files should not wipe the saved weekend/season data.

## Validation

The included test pass confirmed:

- Weekend manager standard flow: PASS
- Weekend manager sprint flow: PASS
- Dashboard HTTP root: PASS
- UDP simulator packet reception: PASS
- UDP parse errors during simulator run: 0
- Persistence after restart: PASS
