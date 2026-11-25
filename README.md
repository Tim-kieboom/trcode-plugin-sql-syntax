# SQL syntax for TerminalCode

Syntax highlighting for SQL (`.sql`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin.

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `sql.wasm`, the tree-sitter grammar built for WebAssembly,
- `manifest.toml`, which says which files are SQL (`[language]`: `extensions`, `comment`) and has the
  highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **SQL**, and turn it on. SQL files are colored when they are opened, and `ctrl+/` comments a line with `--`.

## Where the grammar comes from

The grammar and the query are those of [DerekStride/tree-sitter-sql](https://github.com/DerekStride/tree-sitter-sql) at v0.3.13 (4cd7224)
(MIT, `LICENSE-GRAMMAR`). The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/DerekStride/tree-sitter-sql && cd tree-sitter-sql
git checkout v0.3.13
tree-sitter generate
tree-sitter build --wasm -o sql.wasm
```

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes the first of two patterns on the same text; the grammar's file is written for the last).

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
