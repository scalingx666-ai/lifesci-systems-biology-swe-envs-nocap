# Issue

**Title:** Bump actions/setup-python from 5.0.0 to 5.1.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 5.0.0 to 5.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v5.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Leveraging the raw API to retrieve the version-manifest, as it does not impose a rate limit and hence facilitates unrestricted consumption without the need for a token for Github Enterprise Servers by <a href="https://github.com/Shegox"><code>@​Shegox</code></a> in <a href="">actions/setup-python#766</a>.</li>
<li>Dependency updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a> and <a href="https://github.com/HarithaVattikuti"><code>@​HarithaVattikuti</code></a> in <a href="">actions/setup-python#817</a></li>
<li>Documentation changes for version in README by <a href="https://github.com/basnijholt"><code>@​basnijholt</code></a> in <a href="">actions/setup-python#776</a></li>
<li>Documentation changes for link in README by <a href="https://github.com/ukd1"><code>@​ukd1</code></a> in <a href="">actions/setup-python#793</a></li>
<li>Documentation changes for link in Advanced Usage by <a href="https://github.com/Jamim"><code>@​Jamim</code></a> in <a href="">actions/setup-python#782</a></li>
<li>Documentation changes for avoiding rate limit issues on GHES by <a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> in <a href="">actions/setup-python#835</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/basnijholt"><code>@​basnijholt</code></a> made their first contribution in <a href="">actions/setup-python#776</a></li>
<li><a href="https://github.com/ukd1"><code>@​ukd1</code></a> made their first contribution in <a href="">actions/setup-python#793</a></li>
<li><a href="https://github.com/Jamim"><code>@​Jamim</code></a> made their first contribution in <a href="">actions/setup-python#782</a></li>
<li><a href="https://github.com/Shegox"><code>@​Shegox</code></a> made their first contribution in <a href="">actions/setup-python#766</a></li>
<li><a href="https://github.com/priya-kinthali"><code>@​priya-kinthali</code></a> made their first contribution in <a href="">actions/setup-python#835</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-python/compare/v5.0.0...v5.1.0">https://github.com/actions/setup-python/compare/v5.0.0...v5.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>82c7e63</code></a> Documentation changes for avoiding rate limit issues on GHES (<a href="">#835</a>)</li>
<li><a href=""><code>10aa35a</code></a> feat: fallback to raw endpoint for manifest when rate limit is reached (<a href="">#766</a>)</li>
<li><a href=""><code>9a7ac94</code></a> Bump undici from 5.27.2 to 5.28.3 (<a href="">#817</a>)</li>
<li><a href=""><code>871daa9</code></a> Fix the &quot;Specifying multiple Python/PyPy versions&quot; link (<a href="">#782</a>)</li>
<li><a href=""><code>2f07895</code></a> Fix broken README.md link (<a href="">#793</a>)</li>
<li><a href=""><code>e9d6f99</code></a> Replace setup-python@v4 by setup-python@v5 in README (<a href="">#776</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/v5.0.0...v5.1.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=5.0.0&new-version=5.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce14c5c292c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.