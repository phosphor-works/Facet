<!-- SPDX-FileCopyrightText: 2026 fuddlesworth -->
<!-- SPDX-License-Identifier: GPL-3.0-or-later -->

# Facet

Facet is the one settings app of the phosphor-works suite. Every app plugs its settings into it as a Facet module,
the way a KCM plugs into System Settings. Facet itself is the host: one window, the sidebar, search, Apply, single
instance and deep links. It knows nothing about any one app.

The rules every phosphor-works repository follows come from the workspace repository, imported below. This file adds
Facet's own. The shared Claude Code tooling (the command guard, `phosphor-works:build`, `phosphor-works:code-audit`,
the shared reviewers, the lesson index) comes from the `phosphor-works` plugin, which `.claude/settings.json` enables
and `workspace/tools/setup` installs.

@../workspace/claude/conventions.md

## State

The repository has no code yet. Facet grows out of PlasmaZones' settings app (`plasmazones/src/settings`) and
`phosphor-control` in phosphor-libs, in phase 2 of the Phosphor Split Plan. It leaves PlasmaZones in phase 6c,
after phase 2 step 5 splits the settings app into the host, the placement module and the PlasmaZones module.

## The design

- The module contract lives in `phosphor-control` (core library): a versioned Qt plugin interface plus JSON metadata
  (id, name, icon, category, parent, keywords, order). A module contributes `PageController`s, `StagingDomain`s, its
  QML pages and its search entries.
- Facet loads modules from `<plugindir>/phosphor-works/facet/`. An app's module ships in the app's package and
  depends on `facet` at run time, not at build time. The placement module ships as `phosphor-placement-settings`.
- Each module owns its settings storage and can edit settings whether or not its host runs.
- A page or section is never copied: a module extends another module's pages and categories instead.
- D-Bus is for Facet's single instance and deep links, under `org.phosphor_works`.

## When code lands

Add the layout, the build and test commands, the CI and the app ID to this file. Facet is an app: its code is
`GPL-3.0-or-later`. Add it to the workspace superbuild with a `facet` preset.
