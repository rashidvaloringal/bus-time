# YatraGo – Malappuram Bus Data

A GitHub-ready static version of the YatraGo bus companion demo, connected to the supplied Malappuram bus dataset.

## Files

- `index.html` – YatraGo web app. It loads the matching origin data shard when a user searches.
- `data/*.csv.gz` – CSV data compressed and split by the first character of the origin station. This keeps each data file below GitHub's 100 MB per-file limit and avoids downloading the entire dataset for every search.
- `source/malappuram_bus.db.gz` – compressed copy of the original SQLite database, retained as the source data.
- `data/station-index.json` – maps normalized origin stations to the required data shard(s).
- `data/manifest.json` – row counts and shard information.

## Run locally

Because the app uses `fetch()` to load the data files, do not open `index.html` directly with `file://`.

From this folder, run one of these commands:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## Publish with GitHub Pages

1. Create a new GitHub repository.
2. Upload the contents of this folder (upload `index.html`, `data/`, `source/`, and this README; do not upload the outer ZIP file into the repository).
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select the `main` branch and `/ (root)`, then save.
6. Open the Pages URL shown by GitHub after deployment.

## Data behavior and limitations

- Search currently matches a direct origin-to-destination record in the supplied dataset.
- The app loads only the shard corresponding to the first character of the entered origin.
- Fare, operator, operating-day, and time fields are shown only when present in the source record. Missing values are not fabricated.
- This is timetable/reference data, not live bus tracking or confirmed real-time availability.
- The source database is included for archival/reference purposes; the web app reads the prepared compressed CSV shards.
