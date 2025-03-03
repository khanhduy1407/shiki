# shiki-languages

TextMate grammars for Shiki. Grammars are collected from two sources:

- [VS Code](https://github.com/microsoft/vscode)
- A [handpicked list](/scripts/grammarSources.ts) from GitHub

A [build script](/scripts/pullGrammars.sh) runs every day to pull latest grammars from the upstream sources.

## Supporting your own languages with Shiki

You can add a new language to your shiki instance by using the JSON version of your `tmLanguage` files with the `langs` param in your config:

```ts
import shiki from "shiki"
import {readFileSync} from "fs"

const myLanguageGrammar = JSON.parse(readFileSync("./path/to/lang.tmLanguage.json"))

const myLanguage = {
  id: "mylanguage",
  scopeName: 'source.mylanguage',
  grammar: myLanguageGrammar,
  aliases: ['my', 'mylang'],
}

const highlighter = await shiki.getHighlighter()
await highlighter.loadLanguage(myLanguage)
```

If you just have a `.tmLanguage` and need to convert it to JSON, [this VS Code extension](https://marketplace.visualstudio.com/items?itemName=Togusa09.tmlanguage) can help.

## Adding Grammar

- Find grammar for a language by searching `<lang> textmate` on GitHub or searching `<lang>` on VS Code Marketplace
- Add your grammar to [/scripts/grammarSources.ts](/scripts/grammarSources.ts)
  - Edit `githubGrammarSources` for grammars on a GitHub repository
  - Edit `marketplaceGrammarSources` for grammars found in a VS Code extension. This can be useful when the grammar is compiled and not on GitHub
  - Edit `languageAliases` to allow aliases. For example `md` can refer to `markdown` language
- In [/packages/shiki/samples/](/packages/shiki/samples/), add a code sample file `<id>.sample` for your language. A sample should include a variety of language syntaxes and succinctly capture the idiosyncrasy of a language. Format requirements:
  - Space for indentation
  - Less than 100 columns if possible
  - Link to source in the last line, for example `# From https://poignant.guide/book/chapter-5.html`
- Run `pnpm update:grammars`
- Review the diffs in git. You should see:
  - `docs/languages.md`: Your language id added
  - `packages/shiki/languages/<lang>.tmLanguage.json`: The grammar downloaded
  - `packages/shiki/samples/<lang>.sample`: The sample file you added
  - `packages/shiki/src/languages.ts`: Your language added to `type Lang` and `const languages`
  - `scripts/grammarSources.ts`: The grammar's id and URL
- 🚀 Send in the PR!

## All Languages

```ts
export type Lang =
  | 'abap'
  | 'actionscript-3'
  | 'ada'
  | 'apache'
  | 'apex'
  | 'apl'
  | 'applescript'
  | 'ara'
  | 'asm'
  | 'astro'
  | 'awk'
  | 'ballerina'
  | 'bat' | 'batch'
  | 'beancount'
  | 'berry' | 'be'
  | 'bibtex'
  | 'bicep'
  | 'blade'
  | 'c'
  | 'cadence' | 'cdc'
  | 'clarity'
  | 'clojure' | 'clj'
  | 'cmake'
  | 'cobol'
  | 'codeql' | 'ql'
  | 'coffee'
  | 'cpp' | 'c++'
  | 'crystal'
  | 'csharp' | 'c#' | 'cs'
  | 'css'
  | 'csv'
  | 'cue'
  | 'cypher' | 'cql'
  | 'd'
  | 'dart'
  | 'dax'
  | 'diff'
  | 'docker' | 'dockerfile'
  | 'dream-maker'
  | 'elixir'
  | 'elm'
  | 'erb'
  | 'erlang' | 'erl'
  | 'fish'
  | 'fsharp' | 'f#' | 'fs'
  | 'gdresource'
  | 'gdscript'
  | 'gdshader'
  | 'gherkin'
  | 'git-commit'
  | 'git-rebase'
  | 'glimmer-js' | 'gjs'
  | 'glimmer-ts' | 'gts'
  | 'glsl'
  | 'gnuplot'
  | 'go'
  | 'graphql' | 'gql'
  | 'groovy'
  | 'hack'
  | 'haml'
  | 'handlebars' | 'hbs'
  | 'haskell' | 'hs'
  | 'hcl'
  | 'hjson'
  | 'hlsl'
  | 'html'
  | 'http'
  | 'imba'
  | 'ini' | 'properties'
  | 'java'
  | 'javascript' | 'js'
  | 'jinja-html'
  | 'jison'
  | 'json'
  | 'json5'
  | 'jsonc'
  | 'jsonl'
  | 'jsonnet'
  | 'jssm' | 'fsl'
  | 'jsx'
  | 'julia'
  | 'kdu-html'
  | 'kdu'
  | 'kotlin' | 'kt' | 'kts'
  | 'kusto' | 'kql'
  | 'latex'
  | 'less'
  | 'liquid'
  | 'lisp'
  | 'logo'
  | 'lua'
  | 'make' | 'makefile'
  | 'markdown' | 'md'
  | 'marko'
  | 'matlab'
  | 'mdc'
  | 'mdx'
  | 'mermaid'
  | 'mojo'
  | 'narrat' | 'nar'
  | 'nextflow' | 'nf'
  | 'nginx'
  | 'nim'
  | 'nix'
  | 'nushell' | 'nu'
  | 'objective-c' | 'objc'
  | 'objective-cpp'
  | 'ocaml'
  | 'pascal'
  | 'perl'
  | 'php'
  | 'plsql'
  | 'postcss'
  | 'powerquery'
  | 'powershell' | 'ps' | 'ps1'
  | 'prisma'
  | 'prolog'
  | 'proto'
  | 'pug' | 'jade'
  | 'puppet'
  | 'purescript'
  | 'python' | 'py'
  | 'r'
  | 'raku' | 'perl6'
  | 'razor'
  | 'reg'
  | 'rel'
  | 'riscv'
  | 'rst'
  | 'ruby' | 'rb'
  | 'rust' | 'rs'
  | 'sas'
  | 'sass'
  | 'scala'
  | 'scheme'
  | 'scss'
  | 'shaderlab' | 'shader'
  | 'shellscript' | 'bash' | 'sh' | 'shell' | 'zsh'
  | 'shellsession' | 'console'
  | 'smalltalk'
  | 'solidity'
  | 'sparql'
  | 'splunk' | 'spl'
  | 'sql'
  | 'ssh-config'
  | 'stata'
  | 'stylus' | 'styl'
  | 'svelte'
  | 'swift'
  | 'system-verilog'
  | 'tasl'
  | 'tcl'
  | 'tex'
  | 'toml'
  | 'tsx'
  | 'turtle'
  | 'twig'
  | 'typescript' | 'ts'
  | 'v'
  | 'vb' | 'cmd'
  | 'verilog'
  | 'vhdl'
  | 'viml' | 'vim' | 'vimscript'
  | 'vue-html'
  | 'vue'
  | 'vyper' | 'vy'
  | 'wasm'
  | 'wenyan' | '文言'
  | 'wgsl'
  | 'wolfram' | 'wl'
  | 'xml'
  | 'xsl'
  | 'yaml' | 'yml'
  | 'zenscript'
  | 'zig'
```
