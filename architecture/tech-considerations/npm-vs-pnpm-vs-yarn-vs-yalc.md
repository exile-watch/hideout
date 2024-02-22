---
description: >-
  The good, the bad and everything around package managers regarding exile.watch
  development experience
---

# npm vs pnpm vs yarn vs yalc

<figure><img src="../../.gitbook/assets/exile.watch logo" alt="" width="200"><figcaption><p>exile.watch logo</p></figcaption></figure>

tl;dr: `exile.watch` is using `npm` as it's package manager as it was causing the least issues while not really deteriorating developer experience

***

## npm

### Pros

* Supports multiple-package approach provided through monorepo workspaces creating redundancy
* Package dependencies are saved in root `node_modules` making the architecture click without issues&#x20;

### Cons

* `npm install` is so slow it should be a crime
* `npm link` requires running `npm run build` every time we want to test changes in one of your packages
  * `npm link` itself does not hot reload `node_modules`
  * `npm run build` refreshes linked dependency in consumer

***

## pnpm

### Pros

* `pnpm i` is extremely fast
* `pnpm link` hot reloading works without any issues

### Cons

* When linking a package with consumer, pnpm binary is not included so see [#96](https://github.com/pnpm/pnpm/issues/96) and [#899](https://github.com/pnpm/pnpm/issues/899), so ci fails;&#x20;
  * For local development it's need to do `pnpm dedupe` after `pnpm install`
* Since binaries are not included, `pnpm` decides that it needs to install binaries on its own thus invalidating the architecture making it look like a ridiculously overengineered architecture implementation
* required `--shamefully-hoist` option to make `exile.watch` architecture work

***

## yarn

### Pros

* `yarn i` is extremely fast
* `yarn link` hot reloading works without issues

### Cons

* As with `pnpm`, need `nohoist` option to be passed
* And similarly to `pnpm`, the global `node_modules` on user system was causing a lot of inconsistencies and issues when linking or working on various package versions that depended on each other &#x20;

***

## yalc

### Pros

* Seems to be the most straightforward setup out of all above
* Intuitive API

### Cons

* Chain linking dependencies every time is pure pain
* At times `yalc link` didn't work so had to manually run `publish / add` commands thus requiring aforementioned chain linking
