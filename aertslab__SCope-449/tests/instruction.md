# Issue

**Title:** Bump ws from 7.4.3 to 7.4.6 in /opt/scopeserver/bindserver

## Description

Bumps [ws](https://github.com/websockets/ws) from 7.4.3 to 7.4.6.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/websockets/ws/releases">ws's releases</a>.</em></p>
<blockquote>
<h2>7.4.6</h2>
<h1>Bug fixes</h1>
<ul>
<li>Fixed a ReDoS vulnerability (00c425ec).</li>
</ul>
<p>A specially crafted value of the <code>Sec-Websocket-Protocol</code> header could be used
to significantly slow down a ws server.</p>
<pre lang="js"><code>for (const length of [1000, 2000, 4000, 8000, 16000, 32000]) {
  const value = 'b' + ' '.repeat(length) + 'x';
  const start = process.hrtime.bigint();
<p>value.trim().split(/ *, */);</p>
<p>const end = process.hrtime.bigint();</p>
<p>console.log('length = %d, time = %f ns', length, end - start);
}
</code></pre></p>
<p>The vulnerability was responsibly disclosed along with a fix in private by
<a href="https://github.com/robmcl4">Robert McLaughlin</a> from University of California, Santa Barbara.</p>
<p>In vulnerable versions of ws, the issue can be mitigated by reducing the maximum
allowed length of the request headers using the <a href="https://nodejs.org/api/cli.html#cli_max_http_header_size_size"><code>--max-http-header-size=size</code></a>
and/or the <a href="https://nodejs.org/api/http.html#http_http_createserver_options_requestlistener"><code>maxHeaderSize</code></a> options.</p>
<h2>7.4.5</h2>
<h1>Bug fixes</h1>
<ul>
<li>UTF-8 validation is now done even if <code>utf-8-validate</code> is not installed
(23ba6b29).</li>
<li>Fixed an edge case where <code>websocket.close()</code> and <code>websocket.terminate()</code> did
not close the connection (67e25ff5).</li>
</ul>
<h2>7.4.4</h2>
<h1>Bug fixes</h1>
<ul>
<li>Fixed a bug that could cause the process to crash when using the
permessage-deflate extension (92774377).</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f5297f7</code></a> [dist] 7.4.6</li>
<li><a href=""><code>00c425e</code></a> [security] Fix ReDoS vulnerability</li>
<li><a href=""><code>990306d</code></a> [lint] Fix prettier error</li>
<li><a href=""><code>32e3a84</code></a> [security] Remove reference to Node Security Project</li>
<li><a href=""><code>8c914d1</code></a> [minor] Fix nits</li>
<li><a href=""><code>fc7e27d</code></a> [ci] Test on node 16</li>
<li><a href=""><code>587c201</code></a> [ci] Do not test on node 15</li>
<li><a href=""><code>f672710</code></a> [dist] 7.4.5</li>
<li><a href=""><code>67e25ff</code></a> [fix] Fix case where <code>abortHandshake()</code> does not close the connection</li>
<li><a href=""><code>23ba6b2</code></a> [fix] Make UTF-8 validation work even if utf-8-validate is not installed</li>
<li>Additional commits viewable in <a href="https://github.com/websockets/ws/compare/7.4.3...7.4.6">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=ws&package-manager=npm_and_yarn&previous-version=7.4.3&new-version=7.4.6)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot use these labels` will set the current labels as the default for future PRs for this repo and language
- `@dependabot use these reviewers` will set the current reviewers as the default for future PRs for this repo and language
- `@dependabot use these assignees` will set the current assignees as the default for future PRs for this repo and language
- `@dependabot use this milestone` will set the current milestone as the default for future PRs for this repo and language

You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/aertslab/SCope/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bb5946ff7066`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.