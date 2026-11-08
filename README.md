# wiki

[Kiwix](https://kiwix.org) packages sites like Wikipedia, Stack Overflow and DevDocs as ZIM files, single compressed archives with a built-in search index, for reading offline. `bin/wiki` is a CLI to download, search and read them locally as markdown, for humans and agents.

Needs [uv](https://docs.astral.sh/uv/). Run `bin/wiki install` to add `wiki` to your `PATH`, or use `bin/wiki` directly.

- `wikis.txt`: the wikis to keep, as ZIM names without the build date. `*` matches any text, e.g. `devdocs_en_*`. An optional second column gives a short name, e.g. `devdocs_*` names `devdocs_en_clojure` as `devdocs_clojure`. Start from the example with `cp wikis.example.txt wikis.txt`.
- `sources.txt`: the [Kiwix download](https://download.kiwix.org/zim/) folder for each ZIM name prefix, e.g. `unix.stackexchange.com stack_exchange`. Use it to find names for your own `wikis.txt`.
- `bin/wiki`: wikis go by their short name from `wikis.txt`, or their full name, e.g. `wiktionary_en_all_nopic`. Opening Wikipedia alone takes about 300ms, so the read commands start a background server that keeps the wikis open until 30 minutes after the last call.
  - `install`: add `wiki` to your `PATH`, in the config of your shell (bash, zsh or fish).
  - `skill [dir]`: add a skill for using `wiki` to a skills folder, by default [Claude Code's](https://code.claude.com/docs/en/skills) `~/.claude/skills`, or `$CLAUDE_CONFIG_DIR/skills` when that's set. Run it again after moving the repo.
  - `update [--check]`: download the latest build of each wiki into `zim/`, and delete older builds. With `--check` it only lists the wikis that have a newer build, and their download sizes.
  - `sources`: regenerate `sources.txt`.
  - `list`
  - `search <query> [-n N]`: exact title matches first, then one ranked full-text search across all wikis. `in:<prefix>` limits it to wikis whose name starts with the prefix, e.g. `in:devdocs_clojure`.
  - `outline <wiki>/<path>`: the article's headings, with the size of each section.
  - `get <wiki>/<path> [section]`: the article, or one section of it, as markdown.
  - `open <wiki>[/<path>]`: open the wiki, or an article in it, in the Kiwix app. The wiki must be open in Kiwix for its articles to load.
  - `refs <wiki>/<path>`: the articles it links to.
  - `_refs <wiki>/<path> [-n N]`: the articles that link to it. Needs the wiki indexed first.
  - `index [wiki]`: index the links of one wiki, or of every wiki not indexed yet, into a `.refs.sqlite` file next to the ZIM. It skips wikis that are already indexed, so run it again after `update`. You can stop it any time and run it again to continue. Wikipedia takes a while.


## Reading in Kiwix

The Kiwix app (`brew install --cask kiwix`) reads the files in `zim/` in place.
Open them with File > Open... (⌘O), one at a time, or with the + button in the library's Opened list, several at a time.
`bin/wiki open <wiki>` opens one too.
Once a wiki is open in Kiwix, `bin/wiki open <wiki>/<path>` opens a single article in it, e.g. one you found with `bin/wiki search`.

Kiwix doesn't watch the folder, so after `bin/wiki update` downloads a new build, open the new file and remove the old one.
