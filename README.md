# Design Tokens

Central repository for design tokens used across platform-specific design system implementations.

## Structure

```
design-tokens/
├── tokens.json      # Main entry point — references global and brand token files
├── global.json      # Shared tokens: spacing, typography, borderRadius, shadow
├── black.json       # Black brand tokens: light and dark color sets
├── blue.json        # Blue brand tokens: light and dark color sets
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
  "$metadata": {
    "tokenSetOrder": ["global", "light", "dark"],
    "defaultBrand": "black",
    "brands": ["black", "blue"]
  },
  "global": { "$ref": "./global.json" },
  "brand": {
    "black": { "$ref": "./black.json" },
    "blue": { "$ref": "./blue.json" }
  }
}
```

### global.json

Contains tokens shared across all brands:

```json
{
  "spacing": { "s2": {}, "s4": {}, ... "s64": {} },
  "borderRadius": { "small": {}, "medium": {}, "large": {}, "xl": {}, "round": {} },
  "typography": { "fontFamily": {}, "fontSize": {}, "fontWeight": {}, "heading": {}, "body": {}, "label": {} },
  "shadow": { "small": {}, "medium": {}, "large": {} }
}
```

### black.json / blue.json

Each brand file contains light and dark color sets:

```json
{
  "light": {
    "colors": {
      "text": {},
      "background": {},
      "border": {},
      "icon": {}
    }
  },
  "dark": {
    "colors": {
      "text": {},
      "background": {},
      "border": {},
      "icon": {}
    }
  }
}
```

## Adding New Brands

1. Create a new `<brand>.json` file with `light` and `dark` color sets
2. Add a `$ref` entry under `brand` in `tokens.json`
3. Add the brand name to `$metadata.brands` in `tokens.json`
4. Commit and create a new release/tag

## Consumer Repositories

| Platform | Repository |
|----------|------------|
| iOS | [Design-System-SwiftUI](https://github.com/GobiRajeshKumar/Design-System-SwiftUI) |

## Contributing

1. Make changes to the relevant token file (`global.json`, `black.json`, or `blue.json`)
2. Test locally with consumer repos
3. Create a PR
4. After merge, create a new version tag/release
