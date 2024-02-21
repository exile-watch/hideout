---
description: '@exile-watch/nucleus setup & contribution guide'
---

# Contributing (scripts)

## [Prerequisites](../../../../development/prerequisites.md)

## Development

### 1. [Fork @exile-watch/nucleus repo](https://github.com/exile-watch/nucleus)

### 2. [Create GitHub PAT token](../../../../development/generating-github-pat.md)

### 3. [Create .npmrc file](../../../../development/.npmrc-file.md)&#x20;

### 4. Install dependencies

```bash
# project root
$: nvm use # uses node version that's defined in .nvmrc
$: npm i # install dependencies
```

### 5. Check changes made in [nucleus](../) package locally in [crucible](../../crucible/) project

#### a) Create [nucleus](../) package link

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/nucleus project
</strong># package path e.g. ~/nucleus/packages/encounter-data
$: npm link
</code></pre>

#### b) Build [nucleus](../) package

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/nucleus project
</strong># package path e.g. ~/nucleus/packages/encounter-data
$: npm run build
</code></pre>

#### c) Link [nucleus](../) package in [crucible](../../crucible/) project

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/crucible project
</strong># root path ~/crucible
$: npm link @exile-watch/encounter-data #
</code></pre>

### 6. Conclusion

Not happy with the change? \
Repeat step [#b-build-nucleus-package](./#b-build-nucleus-package "mention") and [#c-link-nucleus-package-in-crucible-project](./#c-link-nucleus-package-in-crucible-project "mention")

Happy with the change? \
Create a new pull request and don't forget to locally unlink modified package:

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/nucleus project
</strong># package path e.g. ~/nucleus/packages/encounter-data
$: npm unlink
</code></pre>

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/crucible project
</strong># root path ~/crucible
$: npm i # this will "revert" linked module to the actual package 
</code></pre>
