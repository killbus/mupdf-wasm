# MuPDF WASM Builder

[![Build MuPDF WASM](https://github.com/killbus/mupdf-wasm/actions/workflows/build.yml/badge.svg)](https://github.com/killbus/mupdf-wasm/actions/workflows/build.yml)
[![Latest Release](https://img.shields.io/github/v/release/killbus/mupdf-wasm)](https://github.com/killbus/mupdf-wasm/releases)

This repository automatically builds the WebAssembly (WASM) version of Artifex's [MuPDF](https://mupdf.com/). It provides a simple way to use `mupdf.js` as a package dependency in modern web projects directly from GitHub.

Builds are automatically published as versioned **[GitHub Releases](https://github.com/killbus/mupdf-wasm/releases)**.

## Usage

You can add this package to your project using `pnpm`, `npm`, or `yarn`. By using the `mupdf@` alias, you can import the package with the clean name `mupdf`.

### Production Usage (Recommended)

For production environments, it is strongly recommended to depend on a specific, immutable version tag. This ensures your project's stability and predictability.

1.  Go to the **[Releases page](https://github.com/killbus/mupdf-wasm/releases)** to find the latest version number (e.g., `1.26.7`).
2.  Install using the version tag and the `mupdf` alias:

    ```bash
    # Replace '1.26.7' with the desired version
    pnpm add mupdf@github:killbus/mupdf-wasm#1.26.7
    ```

### Development / Bleeding-Edge Usage

If you need the absolute latest build for development or testing, you can install directly from the `release` branch.

```bash
pnpm add mupdf@github:killbus/mupdf-wasm#release
```

### Importing in Your Code

After installation, you can import it into your project as an ES Module:

```javascript
import * as mupdf from 'mupdf';

// Your code to use the mupdf library...
```

---

## How It Works

This repository uses a two-workflow GitHub Actions CI/CD setup to automate the build and release process.

*   **`main` branch**: Contains the source code for the builder, including the `package.json` template and the GitHub Actions workflow files.
*   **`release` branch**: Contains only the compiled build artifacts for the latest version. This branch serves as the "rolling release" target.

### The Workflows

1.  **[`build.yml`](./.github/workflows/build.yml): The Builder**
    *   Triggers weekly on a schedule or when run manually.
    *   Determines the latest stable version of `ArtifexSoftware/mupdf` by checking its Git tags' creation dates.
    *   Builds the WASM artifacts using the Emscripten SDK.
    *   Uploads the compiled `dist` directory as an artifact for the next workflow.

2.  **[`release.yml`](./.github/workflows/release.yml): The Releaser**
    *   Triggers automatically upon the successful completion of the `build` workflow.
    *   Downloads the build artifacts.
    *   Pushes the new build files to the `release` branch.
    *   **Creates a new Git tag and a corresponding GitHub Release**, using the MuPDF version number.
    *   Attaches the build artifacts (`.js`, `.wasm`, etc.) as downloadable assets to the GitHub Release.

---

## Building a Specific Version

You can manually trigger a build for any specific MuPDF tag, branch, or commit.

1.  Navigate to the **Actions** tab of this repository.
2.  In the left sidebar, click on the **"Build MuPDF WASM"** workflow.
3.  Above the list of runs, click the **"Run workflow"** dropdown button.
4.  In the **`mupdf_ref`** input field, enter a Git reference (e.g., a tag like `1.24.0`).
5.  Click the green **"Run workflow"** button. The process will build and create a new release for your specified version.

## Source and License

This project builds source code from the official MuPDF repository. MuPDF is licensed under the **GNU Affero General Public License v3.0**. Consequently, any build artifacts produced by this repository are also subject to the terms of the AGPL.
