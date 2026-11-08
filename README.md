# wikis

Local [Kiwix](https://kiwix.org) ZIM wikis, and a CLI to search and read them.

Needs [uv](https://docs.astral.sh/uv/) and [pandoc](https://pandoc.org).

- `wikis.txt`: the wikis to keep, as ZIM names without the build date. `*` matches any text, e.g. `devdocs_en_*`. Start from the example with `cp wikis.example.txt wikis.txt`.
- `sources.txt`: the [Kiwix download](https://download.kiwix.org/zim/) folder for each ZIM name prefix, e.g. `unix.stackexchange.com stack_exchange`. Use it to find names for your own `wikis.txt`. `bin/sources` regenerates it.
- `bin/update`: downloads the latest build of each wiki into `zim/`, and deletes older builds.
- `bin/wiki`: `list`, `search <query> [-n N]`, and `get <wiki>/<path>` to print an article as markdown.

The Kiwix desktop app (`brew install --cask kiwix`) can open the same files in `zim/`.
