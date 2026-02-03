Shaquille O’Neal 2000–01 Play‑By‑Play Stat Engine

This project reconstructs Shaquille O’Neal’s entire 2000–01 NBA season directly from raw play‑by‑play data.
Instead of relying on box scores, the pipeline extracts every major stat by interpreting the event log itself — points, rebounds, assists, steals, blocks, and a Game Score–style metric.

This is an early build of a larger analytics engine designed to scale to multiple players, seasons, and advanced metrics. The long‑term goal is a fully transparent, event‑driven NBA analytics system.

Features
Event‑Driven Stat Extraction
The project parses raw NBA play‑by‑play data and reconstructs Shaq’s statline using actor roles:

PLAYER1_ID → primary actor (shooter, rebounder, fouler, turnover, etc.)

PLAYER2_ID → secondary actor (assister, stealer, fouled player, etc.)

PLAYER3_ID → tertiary actor (blocker, jump‑ball participant, etc.)

Extracted Stats
Points (from cumulative scoring text like (12 PTS))

Rebounds (event‑based "REBOUND")

Assists (Shaq as PLAYER2_ID on made baskets)

Blocks (Shaq as PLAYER3_ID on blocked shots)

Steals (Shaq as PLAYER2_ID on steal events)

Full Game Log
Each game includes:

Points

Rebounds

Assists

Blocks

Steals

Game Score

Game Score Metric
A simplified Game Score is computed using available stats:

Code
GameScore = 
    PTS
    + 0.4 * FGM
    - 0.7 * FGA
    + 0.7 * FTM
    - 0.4 * FTA
    + 0.6 * REB
    + STL
    + 0.7 * AST
    + 0.7 * BLK
Shooting stats default to zero until they are added in a future update.

Example Output
Code
GAME_ID     PTS  AST  REB  BLK  STL  GAMESCORE
20000998     40    8   17    5    3       62.3
20000807     37    6   19    5    3       59.1
20000049     39    4   14    5    0       53.7
20000519     34    4   23    2    1       53.0
...
These statlines match Shaq’s real 2000–01 performance profile.

Project Status: Early Build
This repository represents the first major milestone in a larger analytics engine.
The current version focuses on:

Parsing raw PBP

Extracting core box score stats

Building a Shaq‑only game log

Computing a basic Game Score

Future versions will expand the scope significantly.

Planned Improvements
Field goal attempts/makes (FGA/FGM)

Free throw attempts/makes (FTA/FTM)

Turnovers and fouls

Possession‑level analysis

Rolling averages and visualizations

Offensive engine metric

Comparison to league averages

Lineup and on/off splits

Support for multiple players and seasons

Why This Project Exists
This project blends:

real‑world messy data

basketball knowledge

event‑based reasoning

custom metric creation

reproducible analytics

Reconstructing a player’s season from raw PBP forces a deeper understanding of the structure of NBA data — not just the final numbers.
