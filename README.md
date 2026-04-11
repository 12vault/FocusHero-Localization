# FocusHero Localization

Public translations for the main FocusHero iOS app target.

This repository is intended to be the source of truth for:

- `Localizable.strings`
- `InfoPlist.strings`

Locales currently included:

- `en`
- `es`
- `ja`
- `ko`
- `ru`
- `zh-Hans`

## Scope

This repo currently mirrors the main app target translations only.

It does not include private-only resources such as:

- widget translations
- watch app translations
- app-intents strings outside the main app target

## Recommended Integration With The Private App Repo

Use this repo as a Git submodule inside the private app repo, then copy these `.lproj` folders into the app bundle during the app target build.

This is the least brittle setup because:

- the public repo stays the source of truth
- the private repo pins a specific localization revision
- widget/watch translations can remain private
- you avoid manual copy-paste drift

## Private Repo Setup

Add this repo as a submodule in the private app repo:

```sh
git submodule add git@github.com:12ya/FocusHero-Localization.git Vendor/FocusHero-Localization
git submodule update --init --recursive
```

Then add a Run Script build phase to the main app target only, after `Copy Bundle Resources`:

```sh
set -euo pipefail

LOCALIZATION_ROOT="${SRCROOT}/Vendor/FocusHero-Localization"
APP_RESOURCES_DIR="${TARGET_BUILD_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}"

if [ ! -d "${LOCALIZATION_ROOT}" ]; then
  echo "Missing localization repo at ${LOCALIZATION_ROOT}"
  exit 1
fi

for locale_dir in "${LOCALIZATION_ROOT}"/*.lproj; do
  locale_name="$(basename "${locale_dir}")"
  destination_dir="${APP_RESOURCES_DIR}/${locale_name}"

  mkdir -p "${destination_dir}"
  rsync -a "${locale_dir}/" "${destination_dir}/"
done
```

## Migration Notes

After the build-phase integration is working in the private repo:

- remove the duplicated main app `.lproj` folders from the private repo
- keep widget/watch localization files private for now
- update the submodule when you want newer translations in the app

Example update flow in the private repo:

```sh
git submodule update --remote Vendor/FocusHero-Localization
git add Vendor/FocusHero-Localization
git commit -m "Update app translations"
```

## Contributor Notes

- Edit the files in this repo, not copied files in the private app repo.
- Keep keys aligned across locales.
- If new targets need to be public later, add them as separate directories instead of mixing them into the root layout.
