## Intl.PluralRules API Specification [draft]

### Status

Current Stage:

 * __Stage 4__

Implementation Progress:

 * Polyfill: https://github.com/eemeli/IntlPluralRules

Spec Text:

 * https://rawgit.com/caridy/intl-plural-rules-spec/master/index.html

### Authors

 * Caridy Patiño (@caridy)
 * Eric Ferraiuolo (@ericf)
 * Alex Sexton (@SlexAxton)

### Reviewers

* Daniel Ehrenberg (@littledan)
* Stefan Penner (@stefanpenner)

### Informative

This proposal is based on the LDML spec, C.11 Language Plural Rules:

 * http://unicode.org/reports/tr35/tr35-numbers.html#Language_Plural_Rules

### Prior Art

 * Java: `Class PluralRules`

### Usage

```javascript
let o = new Intl.PluralRules("en", {
    type: "cardinal" // default type
});
console.log(o.select(0)); // "other"
console.log(o.select(1)); // "one"
console.log(o.select(2)); // "other"
```

Support for ordinals is also included:

```javascript
let o = new Intl.PluralRules("en", {
    type: "ordinal"
});
console.log(o.select(11)); // "one"
console.log(o.select(22)); // "two"
console.log(o.select(33)); // "few"
console.log(o.select(44)); // "other"
```

### TODO

 * [x] `new Intl.PluralRules("en").format(1.02);` should produce `"other"`
 * [x] Bikeshed on Intl.PluralRules
 * [x] Spec `pluralCategories` resolution

### Render Spec

```bash
npm install
npm run build
open index.html
```

### Backpointers

 * https://github.com/tc39/ecma402/issues/34
 * https://groups.google.com/forum/#!topic/javascript-globalization/3nFDf5al5hU
