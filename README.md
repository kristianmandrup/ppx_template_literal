# ppx-template-literals

A ppx to facilitate using template literals in ReasonML.
Specifically designed to make it easier to do [lit-html](https://lit-html.polymer-project.org) development easier using ReasonML.

- See blog post on [ReasonML PPX](https://blog.hackages.io/reasonml-ppx-8ecd663d5640)
- See [OCaml Ast_mapper](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_mapper.html)

- [AST helper](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_helper.html)
- [AST iterator](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_iterator.html)

## Status

WIP: not even started!

## OCaml ppx lang extension

- [A Tutorial to OCaml -ppx Language Extensions - June 2018](https://www.victor.darvariu.me/jekyll/update/2018/06/19/ppx-tutorial.html)
- [Simple ppx tutorial](https://github.com/jccampagne/ocaml_ppx_extension_simple_tutorial)
- [A Guide to Extension Points in OCaml](https://whitequark.org/blog/2014/04/16/a-guide-to-extension-points-in-ocaml/)

## Building ppx binary

If you want to build ReasonML files, you need to pass it through a preprocessor with the `pp` flag.

`refmt` is the Reason reformat (it’s made available with the `reason-cli`). It will, in this scenario, print a binary of your ReasonML file.

`-impl` tells the compiler that the `.re` should be considered as a normal `.ml` (OCaml file)

`ocamlc -pp "refmt --print binary" -o outputFile -impl yourReasonFile.re`

We need the OCaml Common modules available.
-I searches for dependencies and the '+' makes it relative to the OCaml directory
\*/
ocamlc -pp “refmt — print binary” -o ppx -I +compiler-libs ocamlcommon.cma -impl ppx_test.re

# Build

```
npm run build
```

# Watch

```
npm run watch
```

# Editor

If you use `vscode`, Press `Windows + Shift + B` it will build automatically
