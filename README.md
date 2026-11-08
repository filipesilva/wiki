# wikis

Local [Kiwix](https://kiwix.org) ZIM wikis, and a CLI to search and read them.

Needs [uv](https://docs.astral.sh/uv/) and [pandoc](https://pandoc.org).

- `wikis.txt`: the wikis to keep, as a Kiwix folder and a ZIM name without its build date.
- `bin/update`: downloads the latest build of each into `zim/`, and deletes older builds.
- `bin/wiki`: `list`, `search <query> [-n N]`, and `get <wiki>/<path>` to print an article as markdown.

The Kiwix desktop app (`brew install --cask kiwix`) can open the same files in `zim/`.
