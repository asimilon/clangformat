# clangformat
Simple BASH script to recursively clang-format a source tree, with option to exclude files.

### Rationale

I wanted a quick and easy way to `clang-format` my source trees, whilst excluding certain files easily.  I saw a lot of repos including a `.clang-format-ignore` file, but I could not work out how to use one with the `clang-format` provided by `homebrew`.

## Setup

edit `clangformat` so that CLANGFMT points to where ever `clang-format` is located on your system (by default it's set to where `clang-format` is installed under macOS using `homebrew`), make sure it is executable (`chmod +x clangformat`) and place it somewhere in your `$PATH` (or update your `$PATH` accordingly).

## Usage

`clangformat --help` for usage details.

`clangformat <directory> --test`
 * show which files will be formatted in `<directory>`.
 * it is advisable to run this once to decide which files should be added to `.clang-format-ignore` before actually formatting the source tree.

`clangformat <directory>`
 * format in place (`clang-format -i`) using the style defined in `.clang-format` recursively through `<directory>`.
 * e.g. `clangformat Source`

### Excluding files

`.clang-format-ignore`
 * should be in the same directory that you issue `clangformat` from.
 * should contain one per line examples of files to ignore, wildcards are allowed, and in fact are wrapped by wildcards by default.
 * e.g. `sqlite3.*` would match `Source/util/sqlite3.c` **and** `Source/libs/include/sqlite3.h`

## Contributing

I'm sure this could be improved upon, my BASH chops aren't all that amazing, but this works for me, so I wanted to share it!  I wouldn't be surprised if it was hugely inefficient on large code bases.  It could almost certainly be improved by being made more flexible.  Another improvement would be to search upwards in the directory hierarchy for the `.clang-format-ignore` file the same way that `clang-format` searches for `.clang-format` if not present in the current directory. Allowing  `.clang-format-ignore` to contain empty lines and perhaps comments would also be useful.  PRs gladly accepted.
