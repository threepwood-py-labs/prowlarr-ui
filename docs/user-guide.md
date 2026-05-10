# User Guide

## Product Scope

Prowlarr UI is a Windows desktop search client for Prowlarr indexers. It focuses on fast searching, duplicate-aware review, and controlled download actions.

Optional Everything integration marks results that already appear on local storage, which helps avoid duplicate downloads.

## Install and First Run

1. Install Python 3.13 or use the portable release package when available.
2. Make sure your Prowlarr instance is reachable from this machine.
3. For a source install, run:

```bat
python scripts\windows\setup_env.py
```

4. Start the GUI:

```bat
pyw scripts\windows\run_app_gui.pyw
```

Use `python scripts\windows\run_app.py` when you want a console window for diagnostics.

## Configure Prowlarr

Prepare:

- Prowlarr base URL, including `http://` or `https://`
- Prowlarr API key from Prowlarr settings
- optional default categories
- optional custom web search URL

After saving settings, run a small known query before using batch actions.

## Configure Everything Integration

Everything is optional. When enabled, it helps detect titles already present on disk.

Supported modes:

- SDK mode: Everything desktop app is running locally.
- HTTP mode: Everything HTTP server is enabled.
- Disabled mode: duplicate marking is skipped.

If duplicate columns remain empty, confirm Everything is running and test the same title in Everything directly.

## Daily Search Workflow

1. Enter a focused search query.
2. Select indexers and categories when you need a narrow result set.
3. Run the search and wait for all selected indexers to return.
4. Sort or filter by quality, size, age, indexer, or duplicate state.
5. Review Everything matches before selecting download candidates.
6. Download a single row first when validating a new configuration.
7. Use batch download only after filters are correct.

## Common Tasks

### Search Across Indexers

Use the main query box, then select indexers and categories. Leave filters broad for discovery, then narrow the visible results.

### Check for Local Duplicates

Enable Everything integration, then run a search. Review duplicate indicators and local match details before downloading.

### Use Bookmarks

Save repeated queries as bookmarks. Use clear names that describe the content or category rather than temporary search text.

### Run Custom Commands

Configure F2/F3/F4 commands only with scripts you trust. Command templates can receive result title and video values, so treat them as user input.

### Download Results

Prefer single-row downloads when validating indexer behavior. For multi-row downloads, filter the table to exactly the intended rows first.

## Settings and Data

Configuration is stored through the app settings system. Runtime logs and download history are kept separately from the source tree.

When troubleshooting, capture the visible status message and any console output from `run_app.py`.

## Safety Notes

- Download actions are sent to Prowlarr/indexer workflows and may trigger downstream clients.
- Batch download applies to all selected or visible rows depending on the action used.
- Custom commands can execute local scripts; use only commands you understand.
- Everything match results are advisory. Confirm paths before assuming a duplicate is safe to skip.

## Troubleshooting Checklist

- If Prowlarr connection fails, verify URL, API key, and network reachability.
- If no results appear, test the query in Prowlarr directly.
- If Everything duplicate checks fail, confirm the configured integration mode.
- If downloads do not start, verify Prowlarr can download the same release from its web UI.
- If a custom command fails, test the command in a terminal with a simple title first.

## Getting Help

When filing an issue, include:

- app version
- Windows version
- whether you used the portable package or source install
- sanitized Prowlarr URL shape, without API keys
- Everything mode, if enabled
- exact query and filters that reproduce the issue
- relevant logs or console output
