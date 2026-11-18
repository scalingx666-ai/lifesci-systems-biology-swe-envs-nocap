# Issue

**Title:** Bump astral-sh/setup-uv from 6 to 7

## Description

Bumps [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) from 6 to 7.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v7.0.0 🌈 node24 and a lot of bugfixes</h2>
<h2>Changes</h2>
<p>This release comes with a load of bug fixes and a speed up. Because of switching from node20 to node24 it is also a breaking change. If you are running on GitHub hosted runners this will just work, if you are using self-hosted runners make sure, that your runners are up to date. If you followed the normal installation instructions your self-hosted runner will keep itself updated.</p>
<p>This release also removes the deprecated input <code>server-url</code> which was used to download uv releases from a different server.
The <a href="https://github.com/astral-sh/setup-uv?tab=readme-ov-file#manifest-file">manifest-file</a> input supersedes that functionality by adding a flexible way to define available versions and where they should be downloaded from.</p>
<h3>Fixes</h3>
<ul>
<li>The action now respects when the environment variable <code>UV_CACHE_DIR</code> is already set and does not overwrite it. It now also finds <a href="https://docs.astral.sh/uv/reference/settings/#cache-dir">cache-dir</a> settings in config files if you set them.</li>
<li>Some users encountered problems that <a href="https://github.com/astral-sh/setup-uv?tab=readme-ov-file#disable-cache-pruning">cache pruning</a> took forever because they had some <code>uv</code> processes running in the background. Starting with uv version <code>0.8.24</code> this action uses <code>uv cache prune --ci --force</code> to ignore the running processes</li>
<li>If you just want to install uv but not have it available in path, this action now respects <code>UV_NO_MODIFY_PATH</code></li>
<li>Some other actions also set the env var <code>UV_CACHE_DIR</code>. This action can now deal with that but as this could lead to unwanted behavior in some edgecases a warning is now displayed.</li>
</ul>
<h3>Improvements</h3>
<p>If you are using minimum version specifiers for the version of uv to install for example</p>
<pre lang="toml"><code>[tool.uv]
required-version = &quot;&gt;=0.8.17&quot;
</code></pre>
<p>This action now detects that and directly uses the latest version. Previously it would download all available releases from the uv repo
to determine the highest matching candidate for the version specifier, which took much more time.</p>
<p>If you are using other specifiers like <code>0.8.x</code> this action still needs to download all available releases because the specifier defines an upper bound (not 0.9.0 or later) and &quot;latest&quot; would possibly not satisfy that.</p>
<h2>🚨 Breaking changes</h2>
<ul>
<li>Use node24 instead of node20 <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#608</a>)</li>
<li>Remove deprecated input server-url <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#607</a>)</li>
</ul>
<h2>🐛 Bug fixes</h2>
<ul>
<li>Respect UV_CACHE_DIR and cache-dir <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#612</a>)</li>
<li>Use --force when pruning cache <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#611</a>)</li>
<li>Respect UV_NO_MODIFY_PATH <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#603</a>)</li>
<li>Warn when <code>UV_CACHE_DIR</code> has changed <a href="https://github.com/jamesbraza"><code>@​jamesbraza</code></a> (<a href="">#601</a>)</li>
</ul>
<h2>🚀 Enhancements</h2>
<ul>
<li>Shortcut to latest version for minimum version specifier <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#598</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>Bump dependencies <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#613</a>)</li>
<li>Fix test-uv-no-modify-path <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#604</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>37802ad</code></a> Fetch uv from Astral's mirror by default (<a href="">#809</a>)</li>
<li><a href=""><code>9f00d18</code></a> chore(deps): bump zizmorcore/zizmor-action from 0.5.0 to 0.5.2 (<a href="">#808</a>)</li>
<li><a href=""><code>fd8f376</code></a> Switch to ESM for source and test, use CommonJS for dist (<a href="">#806</a>)</li>
<li><a href=""><code>f9070de</code></a> Bump deps (<a href="">#805</a>)</li>
<li><a href=""><code>cadb67b</code></a> chore: update known checksums for 0.10.10 (<a href="">#804</a>)</li>
<li><a href=""><code>e06108d</code></a> Use astral-sh/versions as primary version provider (<a href="">#802</a>)</li>
<li><a href=""><code>0f6ec07</code></a> docs: replace copilot instructions with AGENTS.md (<a href="">#794</a>)</li>
<li><a href=""><code>821e5c9</code></a> docs: add cross-client dependabot rollup skill (<a href="">#793</a>)</li>
<li><a href=""><code>6ee6290</code></a> chore(deps): bump versions (<a href="">#792</a>)</li>
<li><a href=""><code>9f332a1</code></a> Add riscv64 architecture support to platform detection (<a href="">#791</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/setup-uv/compare/v6...v7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=astral-sh/setup-uv&package-manager=github_actions&previous-version=6&new-version=7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35c8ebd18582`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.