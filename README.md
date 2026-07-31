# Assessment-Project
### 1. unzip file
# Boxscore Explorer

A small server that reads the CSV snapshots and serves both a JSON API and
server-rendered boxscore pages for baseball and basketball.

## Setup

Requirements: Node 20 or newer and npm (tested on Node 22).

1. Install dependencies:

   ```bash
   npm install
   ```

2. Place the provided CSV snapshots so the layout is:

   ```
   data/
     baseball/    games.csv team_games.csv team_periods.csv
                  player_games.csv teams.csv people.csv venues.csv
     basketball/  games.csv team_periods.csv player_games.csv
                  teams.csv people.csv venues.csv
   ```

3. Start the server:

   ```bash
   npm start
   ```

   Then open http://localhost:3000 and pick a sport, or hit the API directly,
   e.g. http://localhost:3000/api/baseball

To run against data in another location or on another port:

```bash
DATA_DIR=/path/to/data PORT=8080 npm start
```

Other commands:

```bash
npm run headers     # print every CSV's actual column names and row counts
npm run dev         # start with reload on file change
```

If a page renders with blank stat cells, the snapshot's column names differ
from what the adapters expect; `npm run headers` shows the real names, and
each stat's accepted names are declared at the top of
`src/sports/baseball.ts` and `src/sports/basketball.ts`.

## Endpoints

| Route | What it returns |
| --- | --- |
| `GET /api/:sport` | list of games for that sport |
| `GET /api/:sport/:game_id` | everything needed to render that boxscore |
| `GET /:sport` | HTML game list |
| `GET /:sport/:game_id` | HTML boxscore |

