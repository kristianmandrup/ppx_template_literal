# ppx-template-literals

A ppx to facilitate using template literals in ReasonML.
Specifically designed to make it easier to do [lit-html](https://lit-html.polymer-project.org) development easier using ReasonML.

- See blog post on [ReasonML PPX](https://blog.hackages.io/reasonml-ppx-8ecd663d5640)
- See [OCaml Ast_mapper](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_mapper.html)

- [AST helper](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_helper.html)
- [AST iterator](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Ast_iterator.html)

The recent `reason-vscode` release [supports viewing the AST of the ppx under development](https://twitter.com/jaredforsyth/status/1085947362692890625)

[html function](https://github.com/Polymer/lit-html/blob/master/src/lit-html.ts#L54)

```js
/**
 * Interprets a template literal as an HTML template that can efficiently
 * render to and update a container.
 */
export const html = (strings: TemplateStringsArray, ...values: any[]) =>
  new TemplateResult(strings, values, "html", defaultTemplateProcessor);
```

- [Intro to Template Literals](https://flaviocopes.com/javascript-template-literals/)
- [MDN Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [Google: ES6 Template Strings](https://developers.google.com/web/updates/2015/01/ES6-Template-Strings)
- [CSS Tricks: Template Literals](https://css-tricks.com/template-literals/)

## Goal of ppx

Bindings to [html function](https://github.com/Polymer/lit-html/blob/master/src/lit-html.ts#L54) of [lit-html](https://github.com/Polymer/lit-html)

```txt
[@bs.module "lit-html"] external html2: (array(string), 'a, 'b) => someAbstractType = "html";
[@bs.module "lit-html"] external html3: (array(string), 'a, 'b, 'c) => someAbstractType = "html";
```

Input:

```js
[%html"<div>${name} - ${age} </div>"]`
```

Output:

```js
html2(
  [|"<div>", " - ", " </div>" |],
  name,
  age
)
```

When done, this ppx can be used with [bs-lit-html](https://github.com/kristianmandrup/bs-lit-html#usage) to write `lit-html` apps.

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
