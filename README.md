# sf-skills-plugin

A small Claude Code / Cowork **plugin marketplace** that packages Salesforce's public
[`forcedotcom/sf-skills`](https://github.com/forcedotcom/sf-skills) repository into a single
installable plugin called **sf-skills**.

The plugin's content is pulled directly from the upstream public repo, so it includes every
skill under that repo's `skills/` directory: Apex, LWC, metadata, Flows, OmniStudio, Data Cloud,
Agentforce, UI bundles, integrations, diagrams, and more. Nothing is copied or forked here, which
means running a plugin update pulls Salesforce's latest skills automatically.

This repo is just the catalog (the `marketplace.json`). The skills themselves live upstream.

## Install

From Claude Code (or the Cowork plugin manager):

```
/plugin marketplace add ccmalcom/sf-skills-plugin
/plugin install sf-skills@sf-skills-plugin
```

The first command registers this repo as a marketplace. The second clones the upstream repo and
installs all of its skills as one plugin.

> Installing from a local clone instead of GitHub? Point the first command at the folder path:
> `/plugin marketplace add /path/to/sf-skills-plugin`

## Update to the latest upstream skills

```
/plugin update sf-skills
```

This fetches the latest commits from `forcedotcom/sf-skills` on the `main` branch, picking up any
skills Salesforce has added or changed.

## Enable / disable / remove

```
/plugin disable sf-skills@sf-skills-plugin
/plugin enable sf-skills@sf-skills-plugin
/plugin uninstall sf-skills@sf-skills-plugin
```

## How it works

- The catalog entry's `source` is an absolute GitHub reference (`forcedotcom/sf-skills`), so it
  resolves the same way for anyone who adds this marketplace, regardless of their machine.
- The upstream repo has no `.claude-plugin/plugin.json` manifest. That is fine: Claude Code
  auto-discovers skills from the repo's top-level `skills/` directory, so all skills load without
  any changes to Salesforce's repo.
- To pin to a specific commit instead of tracking `main`, add a `"sha": "<commit-sha>"` field to
  the plugin `source` in `.claude-plugin/marketplace.json`.

## Notes for collaborators

This is a personal project, not an official CloudMasonry or Salesforce distribution. Share it with
SF professionals freely. The upstream skills are licensed by Salesforce under BSD-3-Clause (see the
`LICENSE.txt` in their repo); this marketplace wrapper is MIT licensed (see `LICENSE`).
