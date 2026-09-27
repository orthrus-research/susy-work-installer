# susy.work Workbench installer

This is the small static Cloudflare Pages source for the Workbench Linux installer.
The published [`install.sh`](https://susy.work/install.sh) downloads the exact,
SHA-256-pinned [Linux x64 MVP 0.1.2 bundle](https://github.com/orthrus-research/Workbench/releases/tag/linux-x64-mvp-0.1.2)
from GitHub Releases. This site does not bundle Workbench itself.

## Install

On Linux x64 with GNU libc 2.28 or newer, including a compatible WSL2 Linux
shell:

```sh
curl -fsSL https://susy.work/install.sh | bash
```

The installer prints the full path to `workbench-tui` for guided setup. It
installs under the user's data directory, places command shortcuts in
`~/.local/bin`, and configures new Bash and zsh sessions to find them. Open a
new terminal after setup, or run `export PATH="$HOME/.local/bin:$PATH"` in the
current shell. Existing conflicting files are left alone and reported. A repeat
run repairs PATH setup without downloading the bundle.
The [release notes](https://github.com/orthrus-research/Workbench/releases/tag/linux-x64-mvp-0.1.2)
describe the included components and current limits.

## Updating the release

Replace `public/install.sh` with the hook rendered from the exact new bundle.
Regenerate `public/install.sh.sha256`, check the hook's embedded tag, archive
URL, and SHA-256 against the bundle descriptor, and publish the matching GitHub
release asset before deploying the site.

The 0.1.2 PATH correction is a hook-only revision: publish
`workbench-install-linux-x64-path-v2.sh` and `SHA256SUMS-path-v2` as additional
assets on the existing release. Keep its original hook, `SHA256SUMS`, descriptor
and bundle unchanged. The revised hook must still pin that exact bundle;
verify the public asset and checksum before updating `public/install.sh`.

## Cloudflare Pages

The current `susy.work` page is deployed to the temporary Direct Upload Pages
project `susy-work-holding`. The source is committed here for review and
recovery. For a later Git-connected deployment, install the Cloudflare Workers
& Pages GitHub App on `orthrus-research` with access limited to
`susy-work-installer`, then connect this repository to a separate Pages project:

- Production branch: `main`
- Root directory: repository root
- Build command: none
- Build output directory: `public`

Verify the new project's `pages.dev` address and release download before moving
`susy.work` from the temporary project.

This site has no Functions, runtime binding, or login feature. It serves only
the installation page, script, and checksum. The broader website can replace
or extend it in a later release.
