# Asterlyn Hello plugin

This repository is the independently versioned public acceptance fixture for Asterlyn's external
plugin path. It adds one plain command contribution and requests no host permission.

The repository deliberately stays close to the public template. Every Release must:

1. keep `manifest.json`, `package.json`, and the exported runtime identity on the same version;
2. retain the exact `asterlyn-plugin-sdk-1.8.0.tgz` plus checksum from an Asterlyn Release under
   `vendor/`, then commit both the SDK artifact and `package-lock.json`;
3. keep capabilities and permissions empty unless the plugin genuinely needs host authority;
4. run `npm ci && npm run verify`; and
5. push tag `v<version>` only after verification succeeds.

`npm run package:release` creates one deterministic `.asterlyn-plugin.tgz`. `npm run
package:inspect` invokes either `ASTERLYN_PLUGIN_INSPECTOR` or the canonical inspector in
`ASTERLYN_HOST_CHECKOUT`. The included Release workflow pins the oldest compatible host tag and
publishes exactly the inspected package.

Plugin code executes in Asterlyn's supervised plugin-host process. There is no DOM, Tauri, Node,
filesystem, process, network, credential, or shell authority. Host operations are available only
through manifest-admitted capabilities and permissions.

Before adding host authority, read the public [developer
guide](https://github.com/guozhiqiang123/asterlyn/blob/main/docs/plugins/developer-guide.md),
[capability catalog](https://github.com/guozhiqiang123/asterlyn/blob/main/docs/plugins/capabilities-and-permissions.md),
and [diagnostics and migration
guide](https://github.com/guozhiqiang123/asterlyn/blob/main/docs/plugins/diagnostics-and-migration.md).
