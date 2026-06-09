# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is an Obsidian vault template — a starting point for a new vault that comes pre-configured with plugins and settings. There is no build system, test suite, or compiled code. The only content files are Markdown notes and `.obsidian/` configuration.

## Branch Structure

- `master` / `obsidian` — vault content and configuration (what end users interact with)
- `claude-code` — development/iteration branch for changes to the template itself

## Installed Plugins

Two community plugins are bundled under `.obsidian/plugins/`:

- **ignore** — reads `.obsidianignore` (gitignore syntax) and hides matching files from Obsidian's file explorer, search, and graph. The `.obsidianignore` file in the repo root controls this.
- **obsidian-local-rest-api** (Local REST API with MCP) — runs a local HTTPS REST API and MCP server on port `27124` (insecure HTTP on `27123`, disabled by default). This is the bridge that allows Claude Code to read and write vault notes via MCP.

## Key Configuration Notes

### Secrets / `.gitignore`

`.obsidian/plugins/obsidian-local-rest-api/data.json` is excluded from git (see `.gitignore`). This file holds the API key and auto-generated TLS certificate/private key that the REST API plugin creates on first run. Never commit it.

> **Note:** An initial `data.json` was committed in git history (commit `948a208`). If this repo is made public or shared, regenerate the API key and TLS cert from within Obsidian (plugin settings → regenerate) so the committed credentials are no longer valid.

### Local REST API / MCP Server

The plugin exposes the vault at `https://127.0.0.1:27124`. The API key is stored in `data.json` (gitignored). To connect Claude Code to the vault via MCP, configure the MCP server using the plugin's MCP setup instructions and the local API key shown in its settings panel.

## Working With This Repo

Because this is a vault template (not a software project), typical tasks are:

- **Adding/modifying notes** — edit `.md` files directly; Obsidian picks up changes on the fly.
- **Changing core plugin config** — edit `.obsidian/core-plugins.json`.
- **Updating community plugin bundles** — replace files under `.obsidian/plugins/<plugin-id>/`. Never commit `data.json`.
- **Hiding files from Obsidian** — add patterns to `.obsidianignore` (gitignore syntax, processed by the `ignore` plugin).
