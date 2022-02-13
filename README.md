# Build and publish automatically your Java Maven Library to GitHub Packages and Maven Central.

GitHub action to build a Java Maven library and publish it to GitHub Packages and Maven Central. 

## Requirements

- Your project need to use Maven
- [ ] [Create an account on Sonatype](https://issues.sonatype.org/secure/Signup!default.jspa)
- [ ] [Create a JIRA ticket on Sonatype to approve your groupId (io.github.YOUR-GITHUB-USERNAME)](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)
- [ ] [Generate a gpg key and distribute the public key to a keyserver](https://central.sonatype.org/publish/requirements/gpg/)

## GitHub secrets configuration 
- [ ] **Create your GitHub secrets on your repository**
  - *NEXUS_USERNAME* with your username used on Sonatype
  - *NEXUS_PASSWORD* with your password used on Sonatype
  - *GPG_PRIVATE_KEY* with the private key of your generated pgp key
    - to get the private key `gpg --armor --export-secret-key <key-id> > privkey.asc` 
  - *GPG_PASSPHRASE* with the passphrase of your gpg key

## pom.xml configuration
- [ ] **Fix pom.xml**
  - *To guide you, a FIXME tag has been added to all lines to be edited.*


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
          nexus-username: ${{ secrets.NEXUS_USERNAME }}
          nexus-password: ${{ secrets.NEXUS_PASSWORD }}
          gpg-private-key: ${{ secrets.GPG_PRIVATE_KEY }}
          gpg-passphrase: ${{ secrets.GPG_PASSPHRASE }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          java-version: 17
```
