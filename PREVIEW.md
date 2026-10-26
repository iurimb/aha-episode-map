# Local preview

Do not open `index.html` from disk. `fetch("data/...")` does not work from `file://`. Serve the folder instead:

```bat
cd /d E:\Documents\MY_PROJECTS\hrgur-llm-project\aha-episode-map
python -m http.server 8080
```

Then open [http://127.0.0.1:8080/](http://127.0.0.1:8080/).

Stop the server with `Ctrl+C` in that terminal.

Export, git, and GitHub Pages steps are in [README.md](README.md).
