# Design Tokens

Central repository for design tokens used across platform-specific design system implementations.

## Structure

```
design-tokens/
├── tokens.json          # Main entry point
├── design-tokens.json   # Same token entry payload
├── global.json          # Shared foundations: spacing, sizing, radius, animation
├── setmore.json
├── setmore-black.json
├── serviceforge.json
├── answer-connect.json
└── README.md
```

## Usage

This repository serves as the **single source of truth** for design tokens. Consumer repositories (iOS, Android, Web) fetch tokens from this repo and generate platform-specific code.

### Raw URL for tokens.json

**Public repo:**
```
https://raw.githubusercontent.com/GobiRajeshKumar/design-tokens/main/tokens.json
```

### Version Management

Create **releases** or **tags** to version your tokens:

```bash
# Tag a version
git tag v1.0.0
git push origin v1.0.0

# Or create a release on GitHub
```

Consumer repos can detect version changes and only regenerate when tokens are updated.

## Token Structure

`tokens.json` is the main entry point and references the other files:

```json
{
  "global": "./global.json",
  "brands": {
    "setmore": "./setmore.json",
    "setmore-black": "./setmore-black.json",
    "serviceforge": "./serviceforge.json",
    "answer-connect": "./answer-connect.json"
  },
}
```

### global.json

Contains tokens shared across all brands:

```json
{
  "spacing": { "0": "0px", "2": "2px", "...": "..." },
  "sizing": { "0": "0px", "full": "100%" },
  "radius": { "none": "0px", "full": "9999px" },
  "borderWidth": { "regular": "1px", "large": "2px" },
  "animation": { "duration": {}, "easing": {} }
}
```

### Brand files

Each brand file contains typography plus light and dark color schemes:

```json
{
  "typography": {
    "fontFamily": {},
    "fontWeight": {},
    "heading": {},
    "body": {}
  },
  "colorSchemes": {
    "light": {
      "text": {},
      "background": {},
      "border": {},
      "icon": {}
    },
    "dark": {
      "text": {},
      "background": {},
      "border": {},
      "icon": {}
    }
  },
}
```

## Adding New Brands

1. Create a new `<brand>.json` file with `typography` and `colorSchemes`
2. Add the brand file path under `brands` in `tokens.json`
3. Optionally mirror the same entry in `design-tokens.json`
4. Commit and create a new release/tag

## Consumer Repositories

| Platform | Repository |
|----------|------------|
| iOS | [Design-System-SwiftUI](https://github.com/GobiRajeshKumar/Design-System-SwiftUI) |

## Contributing

1. Make changes to the relevant token file (`global.json` or one of the brand JSON files)
2. Test locally with consumer repos
3. Create a PR
4. After merge, create a new version tag/release
