# Territorial Warfare Engine Modifications vs. JSON Mod

The following logic changes are hardcoded in the `core` Kotlin source files. While some behaviors have been "simulated" in the accompanying JSON mod, the true engine modifications provide deeper complexity that standard JSON cannot replicate.

## 1. Imperial Stability Index (ISI)
- **Engine Logic**: Tracks empire stability (0-100) based on expansion, connectivity, and economy.
- **JSON Simulation**: None. ISI is entirely engine-driven.

## 2. Tile Culture & Active Claiming
- **Engine Logic**: Tiles have a `cultureMap`. Units claim ALL tiles traversed.
- **JSON Simulation**: Replicated via `"Gain control over [Unowned] tiles in a [0]-tile radius <upon entering a [All] tile>"`.
- **Limitation**: JSON cannot simulate the slow cultural diffusion or the "rebellion" mechanics.

## 3. Encirclement & Attrition
- **Engine Logic**: Units take **50 HP damage** if they have no pathfinding route to an allied city (Supply Lines).
- **JSON Simulation**: Simulated via `"This Unit takes [50] damage <upon turn end> <in tiles not adjacent to [Friendly] tiles>"`.
- **Limitation**: JSON only checks the 6 immediate neighbors. It doesn't understand "Supply Lines" or being cut off by a 1-tile gap.

## 4. Invader Attrition
- **Engine Logic**: Hardcoded damage when invading foreign territory.
- **JSON Simulation**: Replicated via `"[This Unit] takes [15] damage <upon entering a [Foreign Land] tile>"`.

## 5. Allied Support Bonus
- **Engine Logic**: Tiered bonus (+20% for 2 allies, +40% for 3+).
- **JSON Simulation**: Replicated via adjacency-based Strength uniques in `GlobalUniques.json`.

## 6. Vassalage
- **Engine Logic**: Complex diplomatic status with tribute and war-following logic.
- **JSON Simulation**: None. Vassalage requires deep engine changes to diplomacy.

## 7. Demographic Overhaul
- **Engine Logic**: 2x food accumulation, famine population loss, population cost for units.
- **JSON Simulation**: None. Vanilla Unciv does not support population costs for units via JSON.
