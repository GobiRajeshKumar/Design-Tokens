# Design Tokens

Central repository for design tokens used across platform-specific design system implementations.

## Structure

```
design-tokens/
├── tokens.json      # Main design tokens file
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

```json
{
  "$metadata": {
    "tokenSetOrder": ["global", "light", "dark"],
    "defaultBrand": "black",
    "brands": ["black", "blue"],
    "version": "1.0.0"
  },
  "brands": {
    "<brand-name>": {
      "global": { /* spacing, typography, borderRadius */ },
      "light": { /* colors for light mode */ },
      "dark": { /* colors for dark mode */ }
    }
  }
}
```

## Adding New Brands

1. Add the brand name to `$metadata.brands` array
2. Create a new object under `brands` with `global`, `light`, and `dark` keys
3. Commit and create a new release/tag

## Consumer Repositories

| Platform | Repository |
|----------|------------|
| iOS | [Design-System-SwiftUI](https://github.com/GobiRajeshKumar/Design-System-SwiftUI) |

## Contributing

1. Make changes to `tokens.json`
2. Test locally with consumer repos
3. Create a PR
4. After merge, create a new version tag/release
