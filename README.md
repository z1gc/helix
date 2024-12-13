<div align="center">

<h1>
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo_dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="logo_light.svg">
  <img alt="Helix" height="128" src="logo_light.svg">
</picture>
</h1>

[![Build status](https://github.com/helix-editor/helix/actions/workflows/build.yml/badge.svg)](https://github.com/helix-editor/helix/actions)
[![GitHub Release](https://img.shields.io/github/v/release/helix-editor/helix)](https://github.com/helix-editor/helix/releases/latest)
[![Documentation](https://shields.io/badge/-documentation-452859)](https://docs.helix-editor.com/)
[![GitHub contributors](https://img.shields.io/github/contributors/helix-editor/helix)](https://github.com/helix-editor/helix/graphs/contributors)
[![Matrix Space](https://img.shields.io/matrix/helix-community:matrix.org)](https://matrix.to/#/#helix-community:matrix.org)

</div>

![Screenshot](./screenshot.png)

A [Kakoune](https://github.com/mawww/kakoune) / [Neovim](https://github.com/neovim/neovim) inspired editor, written in Rust.

The editing model is very heavily based on Kakoune; during development I found
myself agreeing with most of Kakoune's design decisions.

For more information, see the [website](https://helix-editor.com) or
[documentation](https://docs.helix-editor.com/).

All shortcuts/keymaps can be found [in the documentation on the website](https://docs.helix-editor.com/keymap.html).

[Troubleshooting](https://github.com/helix-editor/helix/wiki/Troubleshooting)

# Mad Mod

```bash
HELIX_DEFAULT_RUNTIME=$PWD/runtime cargo install --profile opt --locked --path helix-term
```

* add: goto_word_definition
  - goto_definition with goto_word jumps
  - it will now save the jumps, C-o works

* add: goto_word_reference
  - goto_reference with goto_word jumps (two word for whole buffer)

* mod: goto_reference
  - now it shows a symbole name in it within the column's name section, a little bit ugly, but works
  - now it shows a line as well, it might be way slower... and there's no option to turn off :!
  - not very fast now :(

* add: goto_next/prev_function_name
  - bind to key `[n` and `]n`, to navigate to the function's name, suitable for faster `goto_reference` next
  - TODO: textobjects.scm shall be modified for extra language, so there's lots of missing languages
  - can use `tree-sitter parse ...` cli tools for finding the real node of the function name, and place it into textobjects

* mod: global_search
  - for register '/', the global_search will shows up the result immediatly
  - using `Alt-k` to kill the whole string of the global_search prompt (or other prompts as well)
  - TODO: make argument filter general for file picker as well?

* fix: status message overflow issue, this will trigger by selecting a long enough sentence, and press '*' or else, seems openSUSE only

* mod: symbol_picker
  - make LSP support `hierarchicalDocumentSymbolSupport`, and shows the full name with signature
  - TODO: the `workspace/symbol` request seems has no hierarchical symbols

* add: focus_N
  - inspired by ace-window, can now use `:focus X` to focus the window numbered by X
  - each window (or view in helix term), has a little sign about it's number at bottom left status line
  - the window is always sorted by the position (x then y)
  - alternative functions `:focus_insert X` to focus the window, and then enter the insert state

* add: search
  - three options `search.case_sensitive`, `search.whole_word` and `search.regex`
  - add the statusline for the search_config, `r` for regex, `c` for case sensitive, and `w` for whole word search
  - if you add `:toggle-option` to your config file for quick toggling, now it will shows the current's value

* mod: search_selection
  - now it selects a whole word in the beginning
  - if you want to keep the original behavior, use `1*` (or any other number)

* add: format-write
  - use `:m` and `:m!` to format then write (mrite)

* add: global config file
  - support `/etc/helix/config.toml` and `/etc/helix/languages.toml`

* add: insert_raw_tab
  - it inserts a real tab now!

* add: command `E` and `O`
  - they will now edit or open file in the current buffer's directory

Many of the changes is commited arbitrarily, so I squashed them into just single commit.

# Features

- Vim-like modal editing
- Multiple selections
- Built-in language server support
- Smart, incremental syntax highlighting and code editing via tree-sitter

Although it's primarily a terminal-based editor, I am interested in exploring
a custom renderer (similar to Emacs) using wgpu or skulpin.

Note: Only certain languages have indentation definitions at the moment. Check
`runtime/queries/<lang>/` for `indents.scm`.

# Installation

[Installation documentation](https://docs.helix-editor.com/install.html).

[![Packaging status](https://repology.org/badge/vertical-allrepos/helix-editor.svg?exclude_unsupported=1)](https://repology.org/project/helix-editor/versions)

# Contributing

Contributing guidelines can be found [here](./docs/CONTRIBUTING.md).

# Getting help

Your question might already be answered on the [FAQ](https://github.com/helix-editor/helix/wiki/FAQ).

Discuss the project on the community [Matrix Space](https://matrix.to/#/#helix-community:matrix.org) (make sure to join `#helix-editor:matrix.org` if you're on a client that doesn't support Matrix Spaces yet).

# Credits

Thanks to [@jakenvac](https://github.com/jakenvac) for designing the logo!
