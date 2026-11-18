# Issue

**Title:** Bump actions/setup-python from 5.4.0 to 5.6.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 5.4.0 to 5.6.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v5.6.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Workflow updates related to Ubuntu 20.04 by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1065</a></li>
<li>Fix for Candidate Not Iterable Error by <a href="https://github.com/aparnajyothi-y"><code>@​aparnajyothi-y</code></a> in <a href="">actions/setup-python#1082</a></li>
<li>Upgrade semver and <code>@​types/semver</code> by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1091</a></li>
<li>Upgrade prettier from 2.8.8 to 3.5.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1046</a></li>
<li>Upgrade ts-jest from 29.1.2 to 29.3.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1081</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5...v5.6.0">https://github.com/actions/setup-python/compare/v5...v5.6.0</a></p>
<h2>v5.5.0</h2>
<h2>What's Changed</h2>
<h3>Enhancements:</h3>
<ul>
<li>Support free threaded Python versions like '3.13t' by <a href="https://github.com/colesbury"><code>@​colesbury</code></a> in <a href="">actions/setup-python#973</a></li>
<li>Enhance Workflows: Include ubuntu-arm runners, Add e2e Testing for free threaded and Upgrade <code>@​action/cache</code> from 4.0.0 to 4.0.3 by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#1056</a></li>
<li>Add support for .tool-versions file in setup-python by <a href="https://github.com/mahabaleshwars"><code>@​mahabaleshwars</code></a> in <a href="">actions/setup-python#1043</a></li>
</ul>
<h3>Bug fixes:</h3>
<ul>
<li>Fix architecture for pypy on Linux ARM64 by <a href="https://github.com/mayeut"><code>@​mayeut</code></a> in <a href="">actions/setup-python#1011</a>
This update maps arm64 to aarch64 for Linux ARM64 PyPy installations.</li>
</ul>
<h3>Dependency updates:</h3>
<ul>
<li>Upgrade <code>@​vercel/ncc</code> from 0.38.1 to 0.38.3 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1016</a></li>
<li>Upgrade <code>@​actions/glob</code> from 0.4.0 to 0.5.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> in <a href="">actions/setup-python#1015</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/colesbury"><code>@​colesbury</code></a> made their first contribution in <a href="">actions/setup-python#973</a></li>
<li><a href="https://github.com/mahabaleshwars"><code>@​mahabaleshwars</code></a> made their first contribution in <a href="">actions/setup-python#1043</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5...v5.5.0">https://github.com/actions/setup-python/compare/v5...v5.5.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a26af69</code></a> Bump ts-jest from 29.1.2 to 29.3.2 (<a href="">#1081</a>)</li>
<li><a href=""><code>30eafe9</code></a> Bump prettier from 2.8.8 to 3.5.3 (<a href="">#1046</a>)</li>
<li><a href=""><code>5d95bc1</code></a> Bump semver and <code>@​types/semver</code> (<a href="">#1091</a>)</li>
<li><a href=""><code>6ed2c67</code></a> Fix for Candidate Not Iterable Error (<a href="">#1082</a>)</li>
<li><a href=""><code>e348410</code></a> Remove Ubuntu 20.04 from workflows due to deprecation from 2025-04-15 (<a href="">#1065</a>)</li>
<li><a href=""><code>8d9ed9a</code></a> Add e2e Testing for free threaded and Bump <code>@​action/cache</code> from 4.0.0 to 4.0.3 ...</li>
<li><a href=""><code>19e4675</code></a> Add support for .tool-versions file in setup-python (<a href="">#1043</a>)</li>
<li><a href=""><code>6fd11e1</code></a> Bump <code>@​actions/glob</code> from 0.4.0 to 0.5.0 (<a href="">#1015</a>)</li>
<li><a href=""><code>9e62be8</code></a> Support free threaded Python versions like '3.13t' (<a href="">#973</a>)</li>
<li><a href=""><code>6ca8e85</code></a> Bump <code>@​vercel/ncc</code> from 0.38.1 to 0.38.3 (<a href="">#1016</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/v5.4.0...v5.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=5.4.0&new-version=5.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc665e4ce343`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.