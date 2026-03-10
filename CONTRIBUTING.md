## Release Process

Releases are created by building the library, packing it into a tarball, and uploading it to a GitHub release tag.

### Prerequisites

- [GitHub CLI (`gh`)](https://cli.github.com/) installed and authenticated (`gh auth login`)
- `yarn` installed

### Steps

1. **Build the library**

   ```sh
   yarn build
   ```

   This runs `bob build` and outputs compiled JS to `lib/module/` and TypeScript declarations to `lib/typescript/`.

2. **Pack into a tarball**

   ```sh
   yarn pack --filename react-native-track-player-v<version>.tgz
   ```

   Replace `<version>` with the version from `package.json` (e.g. `5.0.0-alpha0`).

3. **Create and push a git tag**

   ```sh
   git tag v<version>
   git push origin v<version>
   ```

4. **Create a GitHub release with the tarball as an asset**

   ```sh
   gh release create v<version> \
     --repo <owner>/<repo> \
     --title "v<version>" \
     --prerelease \               # omit for stable releases
     --notes-file CHANGELOG.md \  # or a dedicated release-notes file
     react-native-track-player-v<version>.tgz
   ```

   The `--prerelease` flag should be used for alpha/beta/nightly builds. Omit it for stable releases.

5. **Clean up**

   ```sh
   rm react-native-track-player-v<version>.tgz
   ```

---

## Commit Message Format

This project utilizes [the Angular Conventional Changelog commit message format](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-angular#commit-message-format).
We use this format to automatically generate our Changelog file.

A commit message consists of a **header**, **body** and **footer**.  The header
has a **type**, **scope** and **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The **header** is mandatory and the **scope** of the header is optional.

### Revert

If the commit reverts a previous commit, it should begin with `revert: `,
followed by the header of the reverted commit. In the body it should say:
`This reverts commit <hash>.`, where the hash is the SHA of the commit being
reverted.

### Type

If the prefix is `feat`, `fix` or `perf`, it will appear in the changelog.
However if there is any [BREAKING CHANGE](#footer), the commit will always
appear in the changelog.

Other prefixes are up to your discretion. Suggested prefixes are `build`, `ci`,
`docs` ,`style`, `refactor`, and `test` for non-changelog related tasks.

Details regarding these types can be found in the official [Angular Contributing
Guidelines](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#type).

### Scope

The scope could be anything specifying place of the commit change. For example
`android`, `ios`, `ts`, `events`, etc...

### Subject

The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

### Body

Just as in the **subject**, use the imperative, present tense: "change" not
"changed" nor "changes". The body should include the motivation for the change
and contrast this with previous behavior.

### Footer

The footer should contain any information about **Breaking Changes** and is also
the place to reference GitHub issues that this commit **Closes**.

**Breaking Changes** should start with the word `BREAKING CHANGE:` with a space
or two newlines. The rest of the commit message is then used for this.

A detailed explanation can be found in this [document](#commit-message-format).
