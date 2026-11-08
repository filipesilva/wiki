# wikis

Local [Kiwix](https://kiwix.org) ZIM wikis, and a CLI to search and read them.

Needs [uv](https://docs.astral.sh/uv/).

- `wikis.txt`: the wikis to keep, as ZIM names without the build date. `*` matches any text, e.g. `devdocs_en_*`. An optional second column gives a short name for `bin/wiki`, e.g. `devdocs_*` names `devdocs_en_clojure` as `devdocs_clojure`. Start from the example with `cp wikis.example.txt wikis.txt`.
- `sources.txt`: the [Kiwix download](https://download.kiwix.org/zim/) folder for each ZIM name prefix, e.g. `unix.stackexchange.com stack_exchange`. Use it to find names for your own `wikis.txt`. `bin/sources` regenerates it.
- `bin/update`: downloads the latest build of each wiki into `zim/`, and deletes older builds.
- `bin/wiki`: read the wikis, for people and agents. Wikis go by their short name from `wikis.txt`, or their full name, e.g. `wiktionary_en_all_nopic`.
  - `list`
  - `search <query> [-n N]`: exact title matches first, then one ranked full-text search across all wikis. `in:<prefix>` limits it to wikis whose name starts with the prefix, e.g. `in:devdocs_clojure`.
  - `outline <wiki>/<path>`: the article's headings, with the size of each section.
  - `get <wiki>/<path> [section]`: the article, or one section of it, as markdown.
  - `open <wiki>[/<path>]`: open the wiki, or an article in it, in the Kiwix app. The wiki must be open in Kiwix for its articles to load.
  - `refs <wiki>/<path>`: the articles it links to.
  - `_refs <wiki>/<path> [-n N]`: the articles that link to it. Needs `index <wiki>` first, which writes a `.refs.sqlite` file next to the ZIM.


## Reading in Kiwix

The Kiwix app (`brew install --cask kiwix`) reads the files in `zim/` in place.
Open them with File > Open... (⌘O), one at a time, or with the + button in the library's Opened list, several at a time.
`bin/wiki open <wiki>` opens one too.
Once a wiki is open in Kiwix, `bin/wiki open <wiki>/<path>` opens a single article in it, e.g. one you found with `bin/wiki search`.

Kiwix doesn't watch the folder, so after `bin/update` downloads a new build, open the new file and remove the old one.
