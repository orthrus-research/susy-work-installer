# susy.work Workbench installer

This is the small static Cloudflare Pages source for the Workbench Linux installer.
The published `install.sh` delegates to an exact, SHA-256-pinned Workbench bundle
on GitHub Releases. It does not bundle Workbench itself.

## Release handoff

Before the first push, replace `public/install.sh` with the script rendered from
the final Workbench release bundle. Regenerate `public/install.sh.sha256` from
that exact file and check the embedded release tag, archive URL, and SHA-256
against the release descriptor. The matching GitHub release asset must exist
before this site is made live.

## Cloudflare Pages

Install the Cloudflare Workers & Pages GitHub App on `orthrus-research` with
access limited to `susy-work-installer`, then connect this repository to a
Cloudflare Pages project:

- Production branch: `main`
- Root directory: repository root
- Build command: none
- Build output directory: `public`

The Pages project can use its `pages.dev` address for preview. Attach
`susy.work` only after the release asset is published and the installer
command is verified there. The domain zone already exists in Cloudflare.

This site has no Functions, runtime binding, or login feature. It serves only
the installation page, script, and checksum. The broader website can replace
or extend it in a later release.
