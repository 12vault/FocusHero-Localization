# FocusHero Localization

Public localization files for the FocusHero iOS app.

This repository contains translations for:

- `Localizable.strings`
- `InfoPlist.strings`

## Locales

- `en`
- `es`
- `ja`
- `ko`
- `ru`
- `zh-Hans`

Each locale lives in its own `.lproj` folder:

```text
en.lproj/
es.lproj/
ja.lproj/
ko.lproj/
ru.lproj/
zh-Hans.lproj/
```

## Contributing

1. Edit the matching files for your locale.
2. Keep the keys exactly the same as the English source.
3. Change only the translated values unless a key is clearly wrong.
4. Preserve escaping, quotes, placeholders, and line breaks.

## Translation Rules

- Do not rename files or locale folders.
- Do not remove keys unless the English source removes them.
- Keep `%@`, `%d`, `%ld`, and similar format placeholders unchanged.
- Keep app names, product names, and branded terms consistent.
- If a string is unclear, open an issue or pull request note instead of guessing.

## Adding A New Language

1. Create a new `<locale>.lproj` folder.
2. Copy `en.lproj/Localizable.strings` into it.
3. Copy `en.lproj/InfoPlist.strings` into it.
4. Translate the values while keeping all keys unchanged.

## Notes

- `en.lproj` is the source of truth for available keys.
- Keep pull requests focused on localization changes only.
