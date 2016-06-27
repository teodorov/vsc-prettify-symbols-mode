# Prettify Symbols Mode

[Prettify Symbols Mode](https://www.emacswiki.org/emacs/PrettySymbol) for [Visual Studio Code (1.3.0)](https://code.visualstudio.com).

Prettify symbols mode makes *visual* substitutions to your source code, e.g. displaying `fun` as `λ`, while never touching your code itself.

**Notice**: *this extension is not yet supported by the public release of vscode; it only works in the insider's build*.

## Configuration

Once you have installed this extension, modify  `settings.json` to add language-specific substitutions. For example, the following settings will target F# files, and will make the following substitutions: `fun` -> `λ` and `->` -> `⟶`.
```json
"prettifySymbolsMode.substitutions": [{
    "language": "fsharp",
    "substitutions": [
      { "ugly": "fun", "pretty": "λ", "pre": "\\b", "post": "\\b" },
      { "ugly": "->", "pretty": "⟶" }
    ]
}]
```

Substitutions work by matching any string that satisfies the `"ugly"` pattern and visually replacing it with `"pretty"`; you can optionally specify the context by providing `"pre"` or `"post"` regular expressions that must be matched for the substitution to occur. You can also target multiple languages or glob patterns at once via `"languages": ["fsharp", {"pattern":  "**/*.txt"}]`.


### Regular expressions

This extension uses [Javascript's regular expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) syntax for `"ugly"`, `"pre"`, and `"post"` (but double-escaped because it is parsed by both JSON and regexp). You must avoid using capturing-groups or mis-parenthesized expressions as it will cause substitutions to behave unpredictably (validation is not performed so you will not receive an error message). 

## Variable-width symbols driving you crazy?

Check out [*Monospacifier*](https://github.com/cpitclaudel/monospacifier) to fix your fonts!

![example fix for variable-width fonts](https://github.com/cpitclaudel/monospacifier/blob/master/demo/symbola-loop.gif?raw=true)

## Known issues: *beta!*

* Cursor movement goes *underneath* the substitution and the cursor will disappear.
  - you can fix cursor movement by respectively binding the left (+shift) and right (+shift) arrow keys to "extension.prettyCursorLeft", "extension.prettyCursorSelectLeft", "extension.prettyCursorRight", and "extension.prettyCursorSelectRight". However, you may notice more lag in cursor movement because of an ongoing issue with vscode.
* You can write bad regular expressions that break substitutions and you will not get an error message.
* Substitutions are only performed on *open* documents, so you may have to begin editing to activate substitutions.
* This extension is only available for version 1.3.0 of vscode (currently an "insider" build).

## Examples

```json
"prettifySymbolsMode.substitutions": [{
  "language": "haskell",
  "substitutions": [
    { "ugly": "\\\\",     "pretty": "λ", "post": "\\s*(?:\\w|_).*?\\s*->" },
    { "ugly": "<-",       "pretty": "←" },
    { "ugly": "->",       "pretty": "→" },
    { "ugly": "==",       "pretty": "≡" },
    { "ugly": "/=",       "pretty": "≢" },
    { "ugly": "\\(\\)",   "pretty": "∅" },
    { "ugly": "sqrt\\s?", "pretty": "√", "pre": "\\b", "post": "\\b" },
    { "ugly": "&&",       "pretty": "∧" },
    { "ugly": "\\|\\|",   "pretty": "∨" },
    { "ugly": "not\\s?",  "pretty": "¬", "pre": "\\b", "post": "\\b" },
    { "ugly": ">",        "pretty": ">", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<",        "pretty": "<", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": ">=",       "pretty": "≥", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<=",       "pretty": "≤", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "alpha",    "pretty": "α", "pre": "\\b", "post": "\\b" },
    { "ugly": "beta",     "pretty": "β", "pre": "\\b", "post": "\\b" },
    { "ugly": "gamma",    "pretty": "γ", "pre": "\\b", "post": "\\b" },
    { "ugly": "delta",    "pretty": "δ", "pre": "\\b", "post": "\\b" },
    { "ugly": "''",       "pretty": "″" },
    { "ugly": "'",        "pretty": "′" },
    { "ugly": "!!",       "pretty": "‼" },
    { "ugly": "\\.\\.",   "pretty": "…" }
  ]},{
  "language": "ocaml",
  "substitutions": [
    { "ugly": "fun",            "pretty": "λ", "pre": "\\b", "post": "\\b" },
    { "ugly": "<-",             "pretty": "←" },
    { "ugly": "->",             "pretty": "→" },
    { "ugly": "=",              "pretty": "=", "pre": "[^<>=!]|^", "post": "[^<>=]|$" },
    { "ugly": "==",             "pretty": "≡" },
    { "ugly": "!=",             "pretty": "≢" },
    { "ugly": "<>",             "pretty": "≠" },
    { "ugly": "\\(\\)",         "pretty": "∅" },
    { "ugly": "sqrt\\s?",       "pretty": "√", "pre": "\\b", "post": "\\b" },
    { "ugly": "&&",             "pretty": "∧" },
    { "ugly": "\\|\\|",         "pretty": "∨" },
    { "ugly": "not\\s?",        "pretty": "¬", "pre": "\\b", "post": "\\b" },
    { "ugly": ">",              "pretty": ">", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<",              "pretty": "<", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": ">=",             "pretty": "≥", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<=",             "pretty": "≤", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "alpha",          "pretty": "α", "pre": "\\b", "post": "\\b" },
    { "ugly": "beta",           "pretty": "β", "pre": "\\b", "post": "\\b" },
    { "ugly": "gamma",          "pretty": "γ", "pre": "\\b", "post": "\\b" },
    { "ugly": "delta",          "pretty": "δ", "pre": "\\b", "post": "\\b" },
    { "ugly": "''",             "pretty": "″" },
    { "ugly": "'",              "pretty": "′" },
    { "ugly": "List[.]for_all", "pretty": "∀", "pre": "\\b", "post": "\\b" },
    { "ugly": "List[.]exists",  "pretty": "∃", "pre": "\\b", "post": "\\b" },
    { "ugly": "List[.]mem",     "pretty": "∈", "pre": "\\b", "post": "\\b" },
    { "ugly": "\\|",            "pretty": "║", "pre": "^\\s+" }
  ]},{
  "language": "fsharp",
  "substitutions": [
    { "ugly": "fun",           "pretty": "λ", "pre": "\\b", "post": "\\b" },
    { "ugly": "<-",            "pretty": "←" },
    { "ugly": "->",            "pretty": "→" },
    { "ugly": "=",             "pretty": "=", "pre": "[^<>=!]|^", "post": "[^<>=]|$" },
    { "ugly": "==",            "pretty": "≡" },
    { "ugly": "!=",            "pretty": "≢" },
    { "ugly": "<>",            "pretty": "≠" },
    { "ugly": "sqrt\\s?",      "pretty": "√", "pre": "\\b", "post": "\\b" },
    { "ugly": "&&",            "pretty": "∧" },
    { "ugly": "\\|\\|",        "pretty": "∨" },
    { "ugly": "not\\s?",       "pretty": "¬", "pre": "\\b", "post": "\\b" },
    { "ugly": ">",             "pretty": ">", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<",             "pretty": "<", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": ">=",            "pretty": "≥", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<=",            "pretty": "≤", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "alpha",         "pretty": "α", "pre": "\\b", "post": "\\b" },
    { "ugly": "beta",          "pretty": "β", "pre": "\\b", "post": "\\b" },
    { "ugly": "gamma",         "pretty": "γ", "pre": "\\b", "post": "\\b" },
    { "ugly": "delta",         "pretty": "δ", "pre": "\\b", "post": "\\b" },
    { "ugly": "''",            "pretty": "″" },
    { "ugly": "'",             "pretty": "′" },
    { "ugly": "List[.]forall", "pretty": "∀", "pre": "\\b", "post": "\\b" },
    { "ugly": "List[.]exists", "pretty": "∃", "pre": "\\b", "post": "\\b" },
    { "ugly": ">>",            "pretty": "≫", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "<<",            "pretty": "≪", "pre": "[^=<>]|^", "post": "[^=<>]|$" },
    { "ugly": "\\|",           "pretty": "║", "pre": "^\\s+" }
  ]}]
```