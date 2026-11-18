# Issue

**Title:** Bump codecov/codecov-action from 3.1.4 to 3.1.5

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 3.1.4 to 3.1.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v3.1.5</h2>
<h2>What's Changed</h2>
<ul>
<li>action.yml: Update to Node.js 20 by <a href="https://github.com/hallabro"><code>@​hallabro</code></a> in <a href="">codecov/codecov-action#1228</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/hallabro"><code>@​hallabro</code></a> made their first contribution in <a href="">codecov/codecov-action#1228</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/codecov/codecov-action/compare/v3.1.4...v3.1.5">https://github.com/codecov/codecov-action/compare/v3.1.4...v3.1.5</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/main/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h2>4.0.0-beta.2</h2>
<h3>Fixes</h3>
<ul>
<li><a href="">#1085</a> not adding -n if empty to do-upload command</li>
</ul>
<h2>4.0.0-beta.1</h2>
<p><code>v4</code> represents a move from the <a href="https://github.com/codecov/uploader">universal uploader</a> to the <a href="https://github.com/codecov/codecov-cli">Codecov CLI</a>. Although this will unlock new features for our users, the CLI is not yet at feature parity with the universal uploader.</p>
<h3>Breaking Changes</h3>
<ul>
<li>No current support for <code>aarch64</code> and <code>alpine</code> architectures.</li>
<li>Tokenless uploading is unsuported</li>
<li>Various arguments to the Action have been removed</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4fe8c5f</code></a> chore(release): bump to 3.1.5</li>
<li><a href=""><code>9140fdc</code></a> action.yml: Update to Node.js 20 (<a href="">#1228</a>)</li>
<li>See full diff in <a href="https://github.com/codecov/codecov-action/compare/v3.1.4...v3.1.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=3.1.4&new-version=3.1.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f5b425c2816`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.