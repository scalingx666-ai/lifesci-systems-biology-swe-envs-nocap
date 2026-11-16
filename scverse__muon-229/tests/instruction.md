# Issue

**Title:** Bump re-actors/alls-green from 1.2.2 to 1.3.0 in the actions-deps group

## Description

Bumps the actions-deps group with 1 update: [re-actors/alls-green](https://github.com/re-actors/alls-green).

Updates `re-actors/alls-green` from 1.2.2 to 1.3.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/re-actors/alls-green/releases">re-actors/alls-green's releases</a>.</em></p>
<blockquote>
<h2>v1.3.0</h2>
<!-- raw HTML omitted -->
<h2>🛡️ What's Unmessed</h2>
<blockquote>
<p>[!caution]</p>
<p>There was a small command injection risk in prior versions. I consider it very low because of the specifics of the action use case. But still, do upgrade, okay?</p>
<p><a href="https://github.com/illera88"><code>@​illera88</code></a><a href="https://github.com/sponsors/max-sixty">💰</a> fixed this <a href="https://docs.zizmor.sh/audits/#template-injection">template injection</a> bug in <a href="">#37</a> by passing inputs via env vars.</p>
<p>See GHSA-gj76-h2ch-5m76 for more detail that was first reported by <a href="https://github.com/Corbynx010"><code>@​Corbynx010</code></a><a href="https://github.com/sponsors/Corbynx010">💰</a> while I was at EuroPython.</p>
</blockquote>
<h2>✨ What's Improved</h2>
<p>I did a bunch of internal refactoring including hints of what <a href="https://github.com/max-sixty"><code>@​max-sixty</code></a><a href="https://github.com/sponsors/max-sixty">💰</a> reported in <a href="">#23</a>. And took a small patch of <a href="https://github.com/krokofant"><code>@​krokofant</code></a><a href="https://github.com/sponsors/krokofant">💰</a> in. This involved a bunch of preparatory infra work with testing infra.</p>
<p>One notable improvement is that now thanks to <a href="https://github.com/tomasr8"><code>@​tomasr8</code></a><a href="https://github.com/sponsors/tomasr8">💰</a>'s and <a href="https://github.com/hugovk"><code>@​hugovk</code></a><a href="https://github.com/sponsors/hugovk">💰</a>'s UX suggestions in <a href="">#31</a>, the gate status output is colored in the console and should be easier to scan in the log output per line. They entries now have leading <code>✓</code>/<code>❌</code> acceptance marks and the actual incoming job outcomes are labeled with <code>🟢</code>/<code>🔴</code>/<code>⬜</code>/<code>⚫</code>.</p>
<h2>🐛 What's Fixed</h2>
<p>The job-statuses summary could print &quot;Some of the allowed to be skipped jobs did not succeed&quot; based on the wrong condition — it's now tied to <code>allowed-skips</code> as intended, not <code>allowed-failures</code>.</p>
<h2>💪 New Contributors</h2>
<ul>
<li><a href="https://github.com/Corbynx010"><code>@​Corbynx010</code></a><a href="https://github.com/sponsors/Corbynx010">💰</a> lurked in GHSA-gj76-h2ch-5m76 before everyone else :wink:</li>
<li><a href="https://github.com/illera88"><code>@​illera88</code></a> made their first contribution in <a href="">#37</a> and GHSA-gj76-h2ch-5m76</li>
<li><a href="https://github.com/krokofant"><code>@​krokofant</code></a> and <a href="https://github.com/max-sixty"><code>@​max-sixty</code></a> first contributed in <a href="">#23</a></li>
<li><a href="https://github.com/tomasr8"><code>@​tomasr8</code></a> and <a href="https://github.com/hugovk"><code>@​hugovk</code></a> in <a href="">#31</a></li>
</ul>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/re-actors/alls-green/compare/v1.2.2...v1.3.0">https://github.com/re-actors/alls-green/compare/v1.2.2...v1.3.0</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz</code></a> <a href="https://stand-with-ukraine.pp.ua">🇺🇦</a></p>
<p><strong>💬 Discuss</strong> <a href="https://bsky.app/profile/did:plc:ve6s3mxkefjaxty3m4fdqumn/post/3mtn27ckwcs2g">on Bluesky 🦋</a>, <a href="https://mastodon.social/@webknjaz/117136385624434132">on Mastodon 🐘</a> and <a href="https://github.com/re-actors/alls-green/discussions/41">on GitHub</a>.</p>
<p><a href="https://github.com/sponsors/webknjaz"><img src="https://img.shields.io/badge/%40webknjaz-transparent?logo=githubsponsors&amp;logoColor=%23EA4AAA&amp;label=Sponsor&amp;color=2a313c" alt="GH Sponsors badge" /></a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b5b5b37</code></a> Merge pull request <a href="">#38</a> from re-actors/pre-commit-ci-update-config</li>
<li><a href=""><code>bd6edd6</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li><a href=""><code>3967c81</code></a> 💅 Make the output easier to scan</li>
<li><a href=""><code>e68df08</code></a> 💅 Style job statuses title with a 🔮</li>
<li><a href=""><code>62d37b2</code></a> 🧪 Unxfail 'success-of-some-allowed-to-skip-or-fail'</li>
<li><a href=""><code>7b5df6d</code></a> 💅 Add a Codecov badge to README</li>
<li><a href=""><code>2410c4c</code></a> 🐛 Correct reporting failed skipped jobs</li>
<li><a href=""><code>6457593</code></a> 💅 Add a GH Sponsors badge</li>
<li><a href=""><code>a617895</code></a> 💅 Add a pre-commit.ci badge</li>
<li><a href=""><code>8de05dc</code></a> 🧪 Force <code>ctrace</code> core in coveragepy</li>
<li>Additional commits viewable in <a href="https://github.com/re-actors/alls-green/compare/05ac9388f0aebcb5727afa17fcccfecd6f8ec5fe...b5b5b37504aa4183270bd3d855c52a67f212be35">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=re-actors/alls-green&package-manager=github_actions&previous-version=1.2.2&new-version=1.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a39f79883603`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.