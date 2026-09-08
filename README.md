# 01 — Vite + React SPA

## What this isolates

Nothing. That is the point.

This is the control case: a Vite + React + TypeScript + Tailwind single-page
application with no server runtime, no native dependency it declares itself, and a
`dev` script that runs Vite. It is the shape every one of these platforms is built
around. If it fails anywhere, the cause is the platform or the import path, not
anything in the code — which makes it the fixture that tells you whether a failure
elsewhere is meaningful.

Run this one first on each platform. A failure here invalidates the other four.

## What our rules predict

| Platform | Prediction | Why                                        |
| -------- | ---------- | ------------------------------------------ |
| Lovable  | works      | Exactly the stack Lovable generates.       |
| Bolt     | works      | Nothing here needs more than a dev server. |
| Replit   | works      | A container runs this trivially.           |
| v0       | works      | React, though not Next.js.                 |
| Base44   | works      | Nothing platform-specific to travel.       |

Two `info` notes appear on every platform, because they apply to any project: that
native dependency detection only reads declared manifests, and how a repository would
reach that platform in the first place.

## Known gap in this prediction

**Tailwind v4 pulls in a native binary that our rules cannot see.**

`@tailwindcss/vite` depends on `@tailwindcss/oxide`, a Rust module that installs a
platform-specific binary. It is a transitive dependency, so it appears in no manifest
in this repository, and `native-addon-dependency` reads manifests only. The scanner
therefore reports a clean "works everywhere" for a project that does contain a native
addon.

This is the limitation the `native-dependency-detection-is-shallow` note warns about,
made concrete in the control case. Whether it matters in practice is an open
question: `@tailwindcss/oxide` also publishes a `wasm32-wasi` build, so a
WebAssembly-only runtime like Bolt's may install it happily. **That is a question
this fixture is uniquely well placed to answer**, so pay attention to whether the
install step succeeds here, not only to whether the preview renders.

## Observed

<!-- Fill this in by hand after running the fixture through each platform.
     Record what happened, not what you expected. Copy error text verbatim.
     Then add a row to ../OBSERVATION-LOG.md. -->

| Platform | Date | Preview started? | Build error? | Notes |
| -------- | ---- | ---------------- | ------------ | ----- |
| Lovable  |      |                  |              |       |
| Bolt     |      |                  |              |       |
| Replit   |      |                  |              |       |
| v0       |      |                  |              |       |
| Base44   |      |                  |              |       |
