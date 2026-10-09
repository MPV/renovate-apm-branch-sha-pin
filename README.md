# apm: SHA pins that follow a branch never update

## Current behavior

[`apm.yml`](apm.yml) pins the `doc-coauthoring` skill of [anthropics/skills](https://github.com/anthropics/skills) to an older commit of its `main` branch, with the branch kept as a trailing comment:

```yaml
- anthropics/skills/skills/doc-coauthoring#b0cbd3df1533b396d281a6886d5132f623393a9c # main
```

anthropics/skills has no tags, so a commit is the only reproducible pin.

Renovate looks the dependency up with the `github-tags` datasource. `main` isn't a version, so Renovate asks for the digest of `main`, and `github-tags` looks for a tag of that name. There is none, so no update is proposed, and the Dependency Dashboard lists:

> Could not determine new digest for update (github-tags package anthropics/skills)

## Expected behavior

A digest update that moves the SHA to the head of `main` and keeps `# main`, as Renovate does for `uses: owner/action@<sha> # main` in GitHub Actions workflows.

## Link to the Renovate issue or Discussion

Not posted yet. The draft is MPV/renovate#25.
