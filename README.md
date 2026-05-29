# canth-modpack

NeoForge 1.21.1 modpack for the Canth Minecraft server, managed with [packwiz](https://packwiz.infra.link/).

## Prerequisites

```bash
go install github.com/packwiz/packwiz@latest
```

## Usage

```bash
# Add a mod from Modrinth
packwiz modrinth install <slug>

# Add a mod from CurseForge
packwiz curseforge install <slug>

# Update all mods
packwiz update --all

# Update a specific mod
packwiz update <slug>

# Remove a mod
packwiz remove <slug>

# Validate and refresh the index
packwiz refresh

# List installed mods
packwiz list

# Export for distribution
packwiz modrinth export -o canth.mrpack
```

## Client-only mods

Tag client-only mods with `side = "client"` in their `.pw.toml` file.
The server's packwiz-installer skips these automatically.

## CI/CD

- **Push to main** — validates the pack, checks index integrity, test export
- **Manual release** — creates a GitHub Release with `.mrpack` and `.zip` exports,
  deploys pack definition to GitHub Pages

## Server integration

The k3s Minecraft server pulls mods via `PACKWIZ_URL` in the itzg Helm chart values:

```yaml
extraEnv:
  PACKWIZ_URL: "https://mwenkdev.github.io/canth-modpack/pack.toml"
```

On pod restart, the server downloads the latest server-side mods automatically.