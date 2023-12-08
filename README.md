# git-cliff-test

## Results

The following modes were tested in two scenarios

- git-cliff was run on HEAD of the `main` branch
- git-cliff was run on the `v2.0.0` tag

For each case the following commands, when applicable, were run:

**Default:** `git-cliff -c .cliff/cliff.toml --strip all`

**Latest:** `git-cliff -c .cliff/cliff.toml --strip all --latest`

**Current:** `git-cliff -c .cliff/cliff.toml --strip all --current`

**Bump:** `git-cliff -c .cliff/cliff.toml --strip all --bump`

**Tag:** `git-cliff -c .cliff/cliff.toml --strip all --tag v4.0.0`

**Unreleased:** `git-cliff -c .cliff/cliff.toml --strip all --unreleased`

Both render and context mode were executed. Outputs are available in the [`results`](results) folder.

For results with respect to HEAD check the subfolder `at_head`. For results with respect to the `v2.0.0` tag check the
subfolder `at_2_0_0`. For render results check `render` and for context results check `context`.

### Run Results on HEAD

We did a diff between the results of the current version (1.4.0) and the new version. The diff was done using the
following command:

```shell
diff -r results/1_4_0/at_head results/new/at_head
```

No differences were found.

### Run Results on Tag

We did a diff between the results of the current version (1.4.0) and the new version. The diff was done using the
following command:

```shell
diff -r results/1_4_0/at_2_0_0 results/new/at_2_0_0
```

The following differences were found:

```diff
diff --color -r results/1_4_0/at_2_0_0/context/current.json results/new/at_2_0_0/context/current.json
31c31
<       "version": null,
---
>       "version": "v1.0.0",
33c33
<       "commit_id": null,
---
>       "commit_id": "fa211a975e7c2a60053561e45660b0c57b847c72",
diff --color -r results/1_4_0/at_2_0_0/render/current.md results/new/at_2_0_0/render/current.md
1c1
< ## [2.0.0](https://github.com/tvcsantos/git-cliff-test/releases/tag/v2.0.0) - 2023-12-08
---
> ## [2.0.0](https://github.com/tvcsantos/git-cliff-test/compare/v1.0.0...v2.0.0) - 2023-12-08
```

We can see that there is a difference for the `--current` mode. On git-cliff 1.4.0 the `--current` mode was not setting
the previous version correctly when running on a checked out tag. This was fixed in the new version.
