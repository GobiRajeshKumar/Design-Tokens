# Design Tokens

Central repository for design tokens used across platform-specific design system implementations.

## Structure

```
design-tokens/
├── tokens.json           # Main entry point
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
  }
}
```

### global.json

Contains shared foundation tokens in DTCG-style format using `$value` and `$type`:

```json
{
  "spacing": {
    "$type": "dimension",
    "4": { "$value": "4px" }
  },
  "animation": {
    "duration": {
      "$type": "duration",
      "200": { "$value": "200ms" }
    }
  }
}
```

### Brand files

Each brand file contains typography plus light and dark color schemes in DTCG-style format:

```json
{
  "typography": {
    "fontFamily": {
      "$type": "fontFamily",
      "heading": { "$value": "Inter" }
    },
    "heading": {
      "16": {
        "$type": "typography",
        "$value": {
          "fontFamily": "{typography.fontFamily.heading}",
          "fontWeight": "600",
          "fontSize": "16px",
          "lineHeight": "24px",
          "letterSpacing": "0px"
        }
      }
    }
  },
  "colorSchemes": {
    "light": {
      "text": {
        "$type": "color",
        "accent": { "$value": "#1d90f5" }
      },
      "shadow": {
        "$type": "shadow",
        "10": {
          "$value": {
            "color": "rgba(0, 0, 0, 0.12)",
            "offsetX": "0px",
            "offsetY": "1px",
            "blur": "4px",
            "spread": "0px"
          }
        }
      }
    }
  }
}
```

## Adding New Brands

1. Create a new `<brand>.json` file with `typography` and `colorSchemes`
2. Add the brand file path under `brands` in `tokens.json`
3. Commit and create a new release/tag

## Consumer Repositories

| Platform | Repository |
|----------|------------|
| iOS | [Design-System-SwiftUI](https://github.com/GobiRajeshKumar/Design-System-SwiftUI) |

## Contributing

1. Make changes to the relevant token file (`global.json` or one of the brand JSON files)
2. Test locally with consumer repos
3. Create a PR
4. After merge, create a new version tag/release
