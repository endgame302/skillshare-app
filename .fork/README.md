# endgame302/skillshare-app fork

This fork publishes **patched Windows builds of runkids/skillshare-app** under the same version numbers.

**Branches:**
- `main` mirrors upstream and gets no fork commits.
- `patched` (the default branch) is the latest upstream release plus the commits below.

**Patches carried:**

| Commit | Upstream status |
|---|---|
| `fix(security): verify the CLI download, add a CSP, update vulnerable deps` | runkids/skillshare-app#136 (that repo only takes PRs from collaborators) |
| `chore(fork): …` (this folder, the release workflow, `SKILLSHARE_CLI_REPO`) | fork only |

**What a fork build changes at build time** (no upstream file is edited for these):
- **App updates** come from this fork's releases, signed with this fork's key. The public key is `.fork/updater.pub`; the private key is in the `TAURI_SIGNING_PRIVATE_KEY` secret.
- **Download CLI** fetches from `endgame302/skillshare`, the patched CLI.

**How a release happens:** `.github/workflows/fork-release.yml` runs every Monday, or by hand.
1. It replays `patched` onto the latest upstream release.
2. It runs the same checks as upstream's `ci.yml`.
3. It builds the NSIS installer on Windows and publishes it with `latest.json`.

**When something fails:** a patch that stops applying, or a failing check, opens an issue and publishes nothing.

**Known gap:** the onboarding's "PowerShell installer" option still runs upstream's `install.ps1`. Use **Download** to get the patched CLI.
