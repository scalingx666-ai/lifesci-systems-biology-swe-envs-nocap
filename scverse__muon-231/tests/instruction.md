# Issue

**Title:** Bump the pre-commit group with 4 updates

## Description

Bumps the pre-commit group with 4 updates: [https://github.com/biomejs/pre-commit](https://github.com/biomejs/pre-commit), [https://github.com/tox-dev/pyproject-fmt](https://github.com/tox-dev/pyproject-fmt), [https://github.com/astral-sh/ruff-pre-commit](https://github.com/astral-sh/ruff-pre-commit) and [https://github.com/zizmorcore/zizmor-pre-commit](https://github.com/zizmorcore/zizmor-pre-commit).

Updates `https://github.com/biomejs/pre-commit` from v2.5.10 to 2.5.11
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c4d01b7</code></a> build(deps): bump <code>@​biomejs/biome</code> to 2.5.11</li>
<li><a href=""><code>22c9100</code></a> build(deps): bump <code>@​biomejs/biome</code> to 2.5.10 (<a href="">#125</a>)</li>
<li>See full diff in <a href="https://github.com/biomejs/pre-commit/compare/055c65a8144b42a1f56908484127aec0c614fb85...c4d01b70e92b66e6a88739145624279889634e92">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/tox-dev/pyproject-fmt` from v2.28.1 to 2.29.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/tox-dev/pyproject-fmt/releases">https://github.com/tox-dev/pyproject-fmt's releases</a>.</em></p>
<blockquote>
<h2>v2.29.0</h2>
<!-- raw HTML omitted -->
<p><strong>Full Changelog</strong>: <a href="https://github.com/tox-dev/pyproject-fmt/compare/v2.28.2...v2.29.0">https://github.com/tox-dev/pyproject-fmt/compare/v2.28.2...v2.29.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bdc5314</code></a> Mirror: 2.29.0</li>
<li><a href=""><code>ac2b9fd</code></a> Mirror: 2.29.0</li>
<li><a href=""><code>b60edd5</code></a> Mirror: 2.28.2</li>
<li><a href=""><code>f4f0065</code></a> Mirror: 2.28.2</li>
<li>See full diff in <a href="https://github.com/tox-dev/pyproject-fmt/compare/cc0b0f8d4107cfe80d6571644e639b05aee29128...bdc53142c79093f52931be2be9aee90756f39f53">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/astral-sh/ruff-pre-commit` from v0.16.4 to 0.16.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff-pre-commit/releases">https://github.com/astral-sh/ruff-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v0.16.5</h2>
<p>See: <a href="https://github.com/astral-sh/ruff/releases/tag/0.16.5">https://github.com/astral-sh/ruff/releases/tag/0.16.5</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1f1e8bf</code></a> Mirror: 0.16.5</li>
<li><a href=""><code>e4c52d6</code></a> Add <code>markdown</code> to <code>types_or</code> (<a href="">#159</a>)</li>
<li><a href=""><code>e602328</code></a> Bump astral-sh/setup-uv from 9.0.0 to 10.0.1 in the github-actions group (<a href="">#180</a>)</li>
<li>See full diff in <a href="https://github.com/astral-sh/ruff-pre-commit/compare/aab412d509121cb5f7533134b7e67f9fab59c682...1f1e8bf348ff38fc88619a38d3ca4d9c56abea49">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/zizmorcore/zizmor-pre-commit` from v1.29.0 to 1.30.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/zizmorcore/zizmor-pre-commit/releases">https://github.com/zizmorcore/zizmor-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v1.30.0</h2>
<p><a href="https://github.com/sponsors/woodruffw/">Sponsorship is appreciated!</a></p>
<h2>New Features 🌈<a href="https://docs.zizmor.sh/release-notes/#new-features">🔗</a></h2>
<ul>
<li>
<p>New audit: <a href="https://docs.zizmor.sh/audits/#self-repository">self-repository</a> detects usages of the old &quot;workspace-relative&quot; form for local reusable workflows and actions and recommends the new &quot;self-repository&quot; form instead (<a href="">#2271</a>)
Enhancements 🌱<a href="https://docs.zizmor.sh/release-notes/#enhancements">🔗</a></p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#impostor-commit">impostor-commit</a> audit now supports pre-commit config inputs (<a href="">#2256</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#forbidden-uses">forbidden-uses</a> audit now supports pre-commit config inputs (<a href="">#2263</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#adhoc-packages">adhoc-packages</a> audit now detects more ad-hoc package management patterns, including bundle add and yarn add</p>
<p>Many thanks to <a href="https://github.com/connorshea"><code>@​connorshea</code></a> for proposing and implementing this enhancement!</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#archived-uses">archived-uses</a> audit now supports pre-commit config inputs (<a href="">#2272</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#ref-confusion">ref-confusion</a> audit now supports pre-commit config inputs (<a href="">#2274</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#cache-poisoning">cache-poisoning</a> audit now produces more detailed and more precise diagnostics (<a href="">#2330</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#cache-poisoning">cache-poisoning</a> audit now handles and exposes auto-fixes in a more general manner (<a href="">#2332</a>)</p>
</li>
<li>
<p>zizmor now recognizes <a href="https://github.com/sethvargo/ratchet">sethvargo/ratchet</a> version comments when evaluating ref pinning (<a href="">#2319</a>)</p>
<p>Many thanks to <a href="https://github.com/njgudman"><code>@​njgudman</code></a> for proposing and implementing this enhancement!</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#unpinned-tools">unpinned-tools</a> audit now produces more detailed and more precise diagnostics (<a href="">#2339</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#unpinned-tools">unpinned-tools</a> audit now detects usages of <a href="https://github.com/extractions/setup-just">extractions/setup-just</a> (<a href="">#2339</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#unpinned-tools">unpinned-tools</a> audit now detects usages of <a href="https://github.com/extractions/setup-crate">extractions/setup-crate</a> (<a href="">#2340</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#archived-uses">archived-uses</a> audit now detects several more archived repositories (<a href="">#2340</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#ref-version-mismatch">ref-version-mismatch</a> audit now supports uses: that reference reusable workflows (<a href="">#2344</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#stale-action-refs">stale-action-refs</a> audit now supports uses: that reference reusable workflows (<a href="">#2345</a>)</p>
</li>
</ul>
<h2>Bug Fixes 🐛<a href="https://docs.zizmor.sh/release-notes/#bug-fixes">🔗</a></h2>
<ul>
<li>
<p>Fixed a bug where zizmor would reject a .pre-commit-config.yml input containing a prek-specific builtin section (<a href="">#2259</a>)</p>
</li>
<li>
<p>Fixed a bug where the <a href="https://docs.zizmor.sh/audits/#unpinned-uses">unpinned-uses</a> audit would fail to honor ignore comments within the same step scope (<a href="">#2289</a>)</p>
</li>
<li>
<p>Fixed a bug where zizmor would reject a dependabot.yml containing a goproxy-server registry definition (<a href="">#2300</a>)</p>
</li>
<li>
<p>Fixed a bug where zizmor would reject pre-commit configurations containing prek-specific glob patterns in files or exclude (<a href="">#2308</a>)</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cef8b83</code></a> Mirror: 1.30.0</li>
<li><a href=""><code>2e74fc1</code></a> Bump astral-sh/setup-uv from 9.0.0 to 10.0.1 in the github-actions group (<a href="">#61</a>)</li>
<li><a href=""><code>7bb2343</code></a> Bump zizmorcore/zizmor-action in the github-actions group (<a href="">#58</a>)</li>
<li><a href=""><code>950796f</code></a> chore: replace pre-commit checks with zizmor-action (<a href="">#57</a>)</li>
<li><a href=""><code>a5dde09</code></a> chore: freeze pin commit hooks, bump usage of own hook (<a href="">#56</a>)</li>
<li><a href=""><code>a21d6cd</code></a> Bump astral-sh/setup-uv from 8.3.2 to 9.0.0 in the github-actions group (<a href="">#55</a>)</li>
<li>See full diff in <a href="https://github.com/zizmorcore/zizmor-pre-commit/compare/451b56af716f9f0d0c2b816503a3fd0cf8b036fa...cef8b8350da46d8114c7e6b7272aebdccdf193ce">compare view</a></li>
</ul>
</details>
<br />

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88c563ef1487`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.