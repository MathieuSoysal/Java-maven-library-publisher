# Build and publish automatically your Java Maven Library to GitHub Packages and Maven Central.

GitHub action to build a Java Maven library and publish it to GitHub Packages and Maven Central. 

## Requirements

- Your project need to use Maven

## Usage

The workflow, usually declared in `.github/workflows/library-publish.yml`, looks like:

```YAML
name: JIB container publish
on:
  release:
    types: [created]
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: JIB container build and publish
        uses: MathieuSoysal/java-maven-publisher@v1.0.0
        with:
          nexus-username:
          nexus-password:
          gpg-private-key:
          gpg-passphrase: 
          github-token: ${{ secrets.GITHUB_TOKEN }}
          java-version: 17
```
