---
description: '@exile-watch/splinters setup & contribution guide'
---

# Contributing

<figure><img src="../../.gitbook/assets/exile.watch logo" alt="" width="200"><figcaption><p>exile.watch logo</p></figcaption></figure>

## [Prerequisites](../../development/prerequisites.md)

## Development

### 1. [Fork @exile-watch/splinters repo](https://github.com/exile-watch/splinters)

### 2. [Create GitHub PAT token](../../development/generating-github-pat.md)

### 3. [Create .npmrc file](../../development/.npmrc-file.md)&#x20;

### 4. Install dependencies

```bash
# project root
$: nvm use # uses node version that's defined in .nvmrc
$: npm i # install dependencies
```

### 5. Check changes made in [splinter](./) package locally in [writ](../writ/) or [crucible](../crucible/) project

#### a) Create [splinter](./) package link

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/splinters project
</strong># package path e.g. ~/splinters/packages/biome-config
$: npm link
</code></pre>

#### b) Build [splinters](./) package

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/splinters project
</strong># package path e.g. ~/splinters/packages/biome-config
$: npm run build
</code></pre>

#### c) Link [splinter](./) package in [crucible](../crucible/)

<pre class="language-bash"><code class="lang-bash"><strong># e.g. @exile-watch/crucible project
</strong># root path ~/crucible
$: npm link @exile-watch/biome-config
</code></pre>

### 6. Conclusion

Not happy with the changes? \
Repeat step [#b-build-splinters-package](contributing.md#b-build-splinters-package "mention") and [#c-link-splinter-package-in-crucible](contributing.md#c-link-splinter-package-in-crucible "mention")

Happy with the change? \
Create a new pull request and don't forget to unlink:

<pre class="language-bash"><code class="lang-bash"><strong># @exile-watch/splinters project
</strong># package path e.g. ~/splinters/packages/biome-config
$: npm unlink
</code></pre>

<pre class="language-bash"><code class="lang-bash"><strong># e.g. @exile-watch/crucible project
</strong># root path ~/crucible
$: npm i # this will "revert" linked module to the actual package 
</code></pre>
