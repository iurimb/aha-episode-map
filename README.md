# Ask Haviv Anything — Episode Map

Static GitHub Pages app: category map, timeline, and title search. It does **not** search inside transcripts (that “study trail of 5 episodes” stays on the local Flask app).

Live data is two JSON files generated from the parent `knowledge_repository` catalog.

## What this site does

- Map of episodes by category (expand / collapse a lane)
- Timeline (time × category)
- Find Episode (substring in the **title**)
- Episode panel: YouTube, themes, summary

## What it does not do

- Transcript search / live 5-episode study trail
- Ingestion, Whisper, or any LLM
- Admin tools

## Update after new episodes (from the parent repo)

The export **does not publish**. It only rewrites JSON in this folder. Pages updates after you push.

```bat
cd /d E:\Documents\MY_PROJECTS\hrgur-llm-project
python -m knowledge_repository.build_repository
python -m knowledge_repository.export_static_pages --output E:\Documents\MY_PROJECTS\hrgur-llm-project\aha-episode-map
cd aha-episode-map
git add data
git commit -m "Refresh episode catalog"
git push
```

Override the destination with `STATIC_PAGES_DIR` if this clone lives somewhere else.

## Local preview

GitHub Pages is the host. To preview on your machine (needed because `fetch("data/...")` does not work from `file://`):

```bat
cd /d E:\Documents\MY_PROJECTS\hrgur-llm-project\aha-episode-map
python -m http.server 8080
```

Open `http://127.0.0.1:8080/`.

## First publish

This folder is a **separate git repo** from `knowledge_repository`. From here:

```bat
git init
git branch -M main
git add .
git commit -m "Initial static episode map"
gh repo create aha-episode-map --public --source=. --remote=origin --push
```

Then on GitHub: **Settings → Pages → Build and deployment** → Source: **Deploy from a branch**, branch **main**, folder **/ (root)**.

URL: `https://<user>.github.io/aha-episode-map/`

Asset fetches are relative (`data/catalog.json`), so the site also works if you later move it under a different Pages project path.
