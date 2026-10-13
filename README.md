# REA upstream synchronization

This isolated controller merges `morluto/rea:main` into `666Abner666/rea:main`.

## Safety
- Keep GitHub Actions **disabled** in the destination repository `666Abner666/rea`. Upstream workflow files are synchronized as files but never executed there.
- The controller does not check out, install, build, or execute REA code.
- GitHub's upstream-merge API preserves fork-only commits and stops on conflicts; no force-push is used.
- Only the `main` branch is synchronized. Tags, GitHub releases, issues, and installed software are not copied.
- The controller's built-in GITHUB_TOKEN has no repository permissions.

## Credential setup
Add the Actions repository secret `REA_SYNC_TOKEN` in **this controller repository**. Use a fine-grained personal access token restricted to **666Abner666/rea only**, with Contents: Read and write and Workflows: Read and write. Metadata: Read-only is required automatically. Do not put the token in files or issues.

Use a bounded expiration (for example 90 days) and replace the secret before expiry. Expiry, revocation, merge conflicts, or repository policy changes can stop synchronization.

## Status and operation
The workflow is currently manual-only while initial credential setup and verification are pending. After a successful test it will be scheduled every 6 hours at minute 37 (UTC).

GitHub can delay scheduled jobs and may disable scheduled workflows in a public repository after 60 days without repository activity. Check the Actions page periodically and re-enable the schedule if GitHub disables it.
