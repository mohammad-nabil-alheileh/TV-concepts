# Localisation (l10n)

Localisation (l10n) means making the app work for different languages and regions. There are three parts:

1. Translated text length
2. Date and number formats
3. Language change at runtime

## a) Translated Text Length

Translations are rarely the same length as English. German and Finnish run 30 to 40% longer, and Arabic can be shorter or longer depending on the phrase. A fixed-width button that fits "Save" may clip "Speichern".

### Rules

- Never hard-code widths on text containers. Use `flex`, `flexShrink`, `padding`, and `minWidth` instead.
- Allow text to wrap.

## b) Date and Number Formats

The same value is written differently in each locale:

| Locale | Number | Notes |
|---|---|---|
| United States (en-US) | `1,234.56` | Comma for thousands, dot for decimals |
| Germany (de-DE) | `1.234,56` | Dot for thousands, comma for decimals |
| Some Arabic locales | `١٬٢٣٤٫٥٦` | Arabic-Indic digits and separators |

Dates, currencies, and plurals also differ between locales.

**Rule:** Don't build these with string concatenation. Use the platform's locale-aware formatting APIs.

## c) Language Change at Runtime

The user switches the language inside the app, without changing the device settings. The app must update its text and formats immediately, without requiring a restart.
