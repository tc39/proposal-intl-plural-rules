# Intl.PluralRules([locales[, options]])

## Rationale

Due to common use, pluralization functions are implemented in a majority of localization libraries. For example, momentjs, react-intl, handlebars-intl, and ember-intl had implemented a form of pluralization to format relative time and ICU Messages.

It is highly probable that the majority of current plural rules implementations are inefficient or required CLDR raw or compiled data to apply the rules. Bringing this into the platform will improve performance of the web, and developer productivity as they no longer have to implement their own pluralization rules.

## Proposal

`Intl.PluralRules` is a low level API to facilitate libraries and frameworks to format ordinals and cardinals in a localized fashion. It is also the first API under `Intl` that is not focused on formatting, but enables access to localization data that is already available in all browsers one way or another.

### Pluralization of Cardinals

The simples example of plural form selection:

```javascript
let pf = new Intl.PluralRules('en');
pf.select(0);    // "other"
pf.select(1);    // "one"
pf.select(11);   // "other"
pf.select(100);  // "other"
```

Arabic has a different rule for cardinals ending on `1`:

```javascript
let pf = new Intl.PluralRules('ar');
pf.select(0);    // "other"
pf.select(1);    // "one"
pf.select(11);   // "one"
pf.select(100);  // "other"
```

### Pluralization of Ordinals

```javascript
let pf = new Intl.PluralRules("en", {
    type: "ordinal"
});
pf.select(11); // "one"   (e.g.: 11st)
pf.select(22); // "two"   (e.g.: 22nd)
pf.select(33); // "few"   (e.g.: 33rd)
pf.select(44); // "other" (e.g.: 44th)
```

## Spec
You can view the [spec text](spec/pluralrules.html) or rendered as [HTML](https://rawgit.com/caridy/intl-plural-rules-spec/master/index.html).

## Naming

Despite the fact that this is a lower level API, we have chosen a similar form than the used for `Intl.NumberFormat` and `Intl.DateTimeFormat`. The creation of `Intl.PluralRules` instance is an expensive operation that requires resolution of locale data, and most likely, libraries will attempt to cache those instances, just like they do for `Intl.NumberFormat`, and `Intl.DateTimeFormat`.

We have also chosen `type` as the primary form of switching between different selection rules. Since this new feature does not format a provided data, just categorize it, we have chosen `.select(value)`.

### Libraries that apply pluralization rules today

Few libraries that would likely get benefited by `Intl.PluralRules` since they will not have to fetch CLDR data to apply pluralization rules by their own:

* momentjs: relative time format (e.g.: `"1 hour ago"` vs `"2 hours ago"`).
* formatjs: ICU messages pluralization rules and relative time format.
* format-message: ICU messages pluralization rules.

### Pluralization rules in other languages

java:

http://icu-project.org/apiref/icu4j/com/ibm/icu/text/PluralFormat.html

```java
Class PluralRulesat

java.lang.Object
  java.text.Format
    com.ibm.icu.text.UFormat
      com.ibm.icu.text.PluralFormat
```

### Annexes

#### ICU messages

Pluralization rules in ICU messages can be resolved by `Intl.PluralRules()`:

```
{ counter, plural,
  one {a meeting}
other {# meetings} }
```
