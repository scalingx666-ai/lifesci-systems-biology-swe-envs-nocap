# Issue

**Title:** Bump actions/setup-python from 5.2.0 to 5.3.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 5.2.0 to 5.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v5.3.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Add workflow file for publishing releases to immutable action package by <a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> in <a href="">actions/setup-python#941</a></li>
<li>Upgrade IA publish by <a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> in <a href="">actions/setup-python#943</a></li>
</ul>
<h3>Bug Fixes:</h3>
<ul>
<li>Normalise Line Endings to Ensure Cross-Platform Consistency by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#938</a></li>
<li>Revise <code>isGhes</code> logic by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/setup-python#963</a></li>
<li>Bump pillow from 7.2 to 10.2.0 by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#956</a></li>
</ul>
<h3>Enhancements:</h3>
<ul>
<li>Enhance workflows and documentation updates by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#965</a></li>
<li>Bump default versions to latest by <a href="https://github.com/jeffwidman"><code>@​jeffwidman</code></a> in <a href="">actions/setup-python#905</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Jcambass"><code>@​Jcambass</code></a> made their first contribution in <a href="">actions/setup-python#941</a></li>
<li><a href="https://github.com/jww3"><code>@​jww3</code></a> made their first contribution in <a href="">actions/setup-python#963</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5...v5.3.0">https://github.com/actions/setup-python/compare/v5...v5.3.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0b93645</code></a> Enhance workflows: Add macOS 13 support, upgrade publish-action, and update d...</li>
<li><a href=""><code>9c76e71</code></a> Bump pillow from 7.2 to 10.2.0 in /<strong>tests</strong>/data  (<a href="">#956</a>)</li>
<li><a href=""><code>f4c5a11</code></a> Revise <code>isGhes</code> logic (<a href="">#963</a>)</li>
<li><a href=""><code>19dfb7b</code></a> Bump default versions to latest (<a href="">#905</a>)</li>
<li><a href=""><code>e9675cc</code></a> Merge pull request <a href="">#943</a> from actions/Jcambass-patch-1</li>
<li><a href=""><code>3226af6</code></a> Upgrade IA publish</li>
<li><a href=""><code>70dcb22</code></a> Merge pull request <a href="">#941</a> from actions/Jcambass-patch-1</li>
<li><a href=""><code>65b48c7</code></a> Create publish-immutable-actions.yml</li>
<li><a href=""><code>29a37be</code></a> initial commit (<a href="">#938</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/v5.2.0...v5.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=5.2.0&new-version=5.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

You can trigger a rebase of this PR by commenting `@dependabot rebase`.

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

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `458dee15a5ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.