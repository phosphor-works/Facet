<!-- SPDX-FileCopyrightText: 2026 Phosphor Works Team -->
<!-- SPDX-License-Identifier: GPL-3.0-or-later -->

<!-- BEGIN shared: tools/sync writes this block from workspace/sync/claude-header.md. Change it there. -->
# Facet

This file has two parts. The rules that every phosphor-works repository follows come first, from the conventions of
the workspace repository, imported below. The sections after them belong to this repository only: what it is, its
layout, how to build and test it, and its own rules, code, skills and agents, and links to the other repositories.
A section here does not repeat a convention. When a section and the conventions disagree, change one of them so
that they agree.

The Claude Code tooling comes from the plugins that `.claude/settings.json` enables and `workspace/tools/setup`
installs. The `phosphor-works` plugin has the command guard, the shared skills (`phosphor-works:build`, `debug`,
`code-audit`, `record-lesson`, `new-repo`), the shared reviewers, and the lesson index, which adds the lessons that
fit each prompt.

@../workspace/claude/conventions.md
<!-- END shared -->

## Overview

Facet is the one settings app of the phosphor-works suite. Every app plugs its settings into it as a Facet module,
the way a KCM plugs into System Settings. Facet itself is the host: one window, the sidebar, search, Apply, single
instance and deep links. It knows nothing about any one app.

### State

The repository has no code yet. Facet grows out of PlasmaZones' settings app (`plasmazones/src/settings`) and
`phosphor-control` in phosphor-libs, in phase 2 of the Phosphor Split Plan. It leaves PlasmaZones in phase 6c,
after phase 2 step 5 splits the settings app into the host, the placement module and the PlasmaZones module.

### The design

- The module contract lives in `phosphor-control` (core library): a versioned Qt plugin interface plus JSON metadata
  (id, name, icon, category, parent, keywords, order). A module contributes `PageController`s, `StagingDomain`s, its
  QML pages and its search entries.
- Facet loads modules from `<plugindir>/phosphor-works/facet/`. An app's module ships in the app's package and
  depends on `facet` at run time, not at build time. The placement module ships as `phosphor-placement-settings`.
- Each module owns its settings storage and can edit settings whether or not its host runs.
- A page or section is never copied: a module extends another module's pages and categories instead.
- D-Bus is for Facet's single instance and deep links, under `org.phosphor_works`.

## Layout

There is no code yet, so there is no layout to describe.

## Build and test

There is no build, no CI and no tests yet.

## Rules

### When code lands

Add the layout, the build and test commands, the CI and the app ID to this file. Facet is an app: its code is
`GPL-3.0-or-later`. Add it to the workspace superbuild with a `facet` preset.
