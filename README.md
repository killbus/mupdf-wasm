# MuPDF WASM Builder

[![Build MuPDF WASM](https://github.com/killbus/mupdf-wasm/actions/workflows/build.yml/badge.svg)](https://github.com/killbus/mupdf-wasm/actions/workflows/build.yml)
[![Latest Release](https://img.shields.io/github/v/release/killbus/mupdf-wasm)](https://github.com/killbus/mupdf-wasm/releases)

This repository automatically builds the WebAssembly (WASM) version of Artifex's [MuPDF](https://mupdf.com/). It provides a simple way to use `mupdf.js` as a package dependency in modern web projects directly from GitHub.

Builds are automatically triggered **weekly** and published as versioned **[GitHub Releases](https://github.com/killbus/mupdf-wasm/releases)**.

## Installation & Usage

You can install this package using `pnpm`, `npm`, or `yarn`. We recommend using the `mupdf` alias for cleaner imports.

### 1. Stable Release (Recommended)

For production environments, use the latest stable version.

```bash
# Install specific version (Recommended for stability)
pnpm add mupdf@github:killbus/mupdf-wasm#v1.25.0

# OR Install from the rolling stable branch
pnpm add mupdf@github:killbus/mupdf-wasm#release
```

### 2. Prerelease / Beta

To test upcoming features from MuPDF release candidates.

```bash
# Install specific release candidate
pnpm add mupdf@github:killbus/mupdf-wasm#v1.26.0-rc1

# OR Install from the rolling beta branch
pnpm add mupdf@github:killbus/mupdf-wasm#release-beta
```

### 3. Nightly Build

To use the absolute latest code from the upstream `master` branch (updated weekly).

```bash
# Install specific nightly build
pnpm add mupdf@github:killbus/mupdf-wasm#nightly-2025.12.08-0bf523c

# OR Install from the rolling nightly branch
pnpm add mupdf@github:killbus/mupdf-wasm#release-nightly
```

### Importing in Your Code

```javascript
import * as mupdf from 'mupdf';

// Your code to use the mupdf library...
```

---

## How It Works

This repository uses a sophisticated GitHub Actions pipeline to automate the build and release process.

### Automated Weekly Builds (`cron`)
Every Sunday, the workflow automatically:
1.  Checks upstream [ArtifexSoftware/mupdf](https://github.com/ArtifexSoftware/mupdf) for updates.
2.  Builds **three variants** in parallel:
    *   **Stable**: Latest official release tag.
    *   **Prerelease**: Latest RC/Beta tag (if available).
    *   **Latest**: The current HEAD of the `master` branch.
3.  Publishes artifacts to separate release channels.

### Release Channels

| Channel | Branch | Tag Pattern | Description |
| :--- | :--- | :--- | :--- |
| **Stable** | `release` | `v1.x.x` | Use for Production. |
| **Beta** | `release-beta` | `v1.x.x-rcX` | Use for testing upcoming releases. |
| **Nightly** | `release-nightly` | `nightly-yyyy.mm.dd-hash` | Bleeding edge from master. |

---

## Manual Builds

You can manually trigger a build at any time via the **Actions** tab:

1.  Select **"Build MuPDF WASM"** workflow.
2.  Click **"Run workflow"**.
3.  Choose a **Build Type**:
    *   `stable` / `prerelease` / `latest`: Builds a single specific variant.
    *   `all`: Builds ALL variants immediately.
4.  (Optional) **Version Override**:
    *   Enter a specific tag (e.g., `1.24.0`), branch, or commit hash to build exactly that version.
    *   Leave empty to auto-resolve based on the Build Type.

## Source and License

This project builds source code from the official MuPDF repository. MuPDF is licensed under the **GNU Affero General Public License v3.0**. Consequently, any build artifacts produced by this repository are also subject to the terms of the AGPL.
