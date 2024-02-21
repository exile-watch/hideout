# Generating GitHub PAT

Instructions for generating a `GitHub PAT` (Personal Access Token) can be found [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token).

Apart from naming your token, no additional modifications are necessary on your part.

Ensure that `Repository access` includes `Public Repositories (read-only)` checked.

***

`exile.watch` packages utilize the `GitHub NPM registry`.

Working with the `GitHub NPM registry` requires tokens with `read` permission. Therefore, a `PAT` is needed, even if you only wish to access public repositories (a.k.a. public packages)
