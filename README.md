## `Intl.PluralForm` API Specification [draft]

This proposal is based on the Unicode Language Plural Rules:

 * http://unicode.org/reports/tr35/tr35-numbers.html#Language_Plural_Rules

### Example

```javascript
let o = new Intl.PluralForm("en", {
    style: "cardinal" // default style
});
console.log(o.resolve(0)); // "other"
console.log(o.resolve(1)); // "one"
console.log(o.resolve(2)); // "other"
```

Support for ordinals is also included:

```javascript
let o = new Intl.PluralForm("en", {
    style: "ordinal"
});
console.log(o.resolve(11)); // "one"
console.log(o.resolve(22)); // "two"
console.log(o.resolve(33)); // "few"
console.log(o.resolve(44)); // "other"
```

### Usage

```
npm install
npm run build
open index.html
```

### Details about this proposal

 * https://github.com/tc39/ecma402/issues/34
 * https://groups.google.com/forum/#!topic/javascript-globalization/3nFDf5al5hU
