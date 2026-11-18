# Issue

**Title:** Bump actions/setup-python from 2 to 3.1.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 2 to 3.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>Support caching poetry dependencies and caching on GHES 3.5</h2>
<ul>
<li>In the scope of this release, we added <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/362">support for caching from GHES 3.5</a> and fixed the download issue for files &gt; 2GB during restore.</li>
<li>Caching poetry dependencies</li>
</ul>
<pre lang="yaml"><code>steps:
- uses: actions/checkout@v3
- name: Install poetry
  run: pipx install poetry
- uses: actions/setup-python@v3
  with:
    python-version: '3.9'
    cache: 'poetry'
- run: poetry install
- run: poetry run pytest
</code></pre>
<h2>v3.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node16 (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/340">actions/setup-python#340</a>)</li>
<li>Update <code>package-lock.json</code> file version to 2, <code>@types/node</code> to 16.11.25 and <code>typescript</code> to 4.2.3 (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/341">actions/setup-python#341</a>)</li>
<li>Remove legacy <code>pypy2</code> and <code>pypy3</code> keywords (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/342">actions/setup-python#342</a>)</li>
</ul>
<h3>Breaking Changes</h3>
<p>With the update to Node 16, all scripts will now be run with Node 16 rather than Node 12.</p>
<p>This new major release removes support of legacy <code>pypy2</code> and <code>pypy3</code> keywords. Please use more specific and flexible syntax to specify a PyPy version:</p>
<pre lang="yaml"><code>jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version:
        - 'pypy-2.7' # the latest available version of PyPy that supports Python 2.7
        - 'pypy-3.8' # the latest available version of PyPy that supports Python 3.8
        - 'pypy-3.8-v7.3.8' # Python 3.8 and PyPy 7.3.8
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v3
      with:
        python-version: ${{ matrix.python-version }}
</code></pre>
<p>See more usage examples in the <a href="https://github.com/actions/setup-python#specifying-a-pypy-version">documentation</a></p>
<h2>Update primary and restore keys for pip</h2>
<p>In scope of this release we <a href="https://github-redirect.dependabot.com/actions/setup-python/pull/303">include a version of python in restore and primary cache keys for pip</a>. Besides, we add temporary fix for Windows caching <a href="https://github-redirect.dependabot.com/actions/setup-python/pull/332">issue</a>, that the <code>pip cache dir</code> command returns non zero exit code or writes to stderr. Moreover we updated <a href="https://github-redirect.dependabot.com/actions/setup-python/pull/327">node-fetch dependency</a>.</p>
<h2>Update actions/cache version to 1.0.8</h2>
<p>We have updated <a href="https://github.com/actions/toolkit/blob/main/packages/cache/RELEASES.md#108">actions/cache</a> dependency version to 1.0.8 to support 10GB cache upload</p>
<h2>Support caching dependencies</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9c644ca</code></a> Update README.md to fix setup-python version  in example (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/368">#368</a>)</li>
<li><a href=""><code>3e8e90e</code></a> dist fix (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/367">#367</a>)</li>
<li><a href=""><code>05fb98d</code></a> Cache on ghes (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/363">#363</a>)</li>
<li><a href=""><code>6c56602</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/281">#281</a> from patrick91/feature/poetry-caching</li>
<li><a href=""><code>9516be8</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/358">#358</a> from actions/brcrista/codeql-main</li>
<li><a href=""><code>7aa3e95</code></a> Update dist</li>
<li><a href=""><code>6c31eb3</code></a> Use <code>\n</code> instead of <code>os.EOL</code></li>
<li><a href=""><code>7a37d78</code></a> Update dist</li>
<li><a href=""><code>e4be7a4</code></a> Initialise pyproject.toml</li>
<li><a href=""><code>aac0ef9</code></a> Build and format</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/v2...v3.1.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=2&new-version=3.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d81903046951`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.