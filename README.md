# Build and publish automatically your Java Maven Library to GitHub Packages and Maven Central.

GitHub action to build a Java Maven library and publish it to GitHub Packages and Maven Central. 

## Requirements

- Your project need to use Maven
- [ ] [Create an account on Sonatype](https://issues.sonatype.org/secure/Signup!default.jspa)
- [ ] [Create a JIRA ticket on Sonatype to approve your groupId (io.github.YOUR-GITHUB-USERNAME)](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)
- [ ] [Generate a gpg key and distribute the public key to a keyserver](https://central.sonatype.org/publish/requirements/gpg/)

## Configurations

### GitHub secrets 
Create your GitHub secrets on your repository:
- [ ] **NEXUS_USERNAME** with your username used on Sonatype
- [ ] **NEXUS_PASSWORD** with your password used on Sonatype
- [ ] **GPG_PRIVATE_KEY** with the private key of your generated pgp key
  - to get the private key `gpg --armor --export-secret-key <key-id> > privkey.asc` 
- [ ] **GPG_PASSPHRASE** with the passphrase of your gpg key

### pom.xml
Inside your *pom.xml* file you need to set:
- [ ] [**the good *groupId*** (io.github.YOUR-GITHUB-USERNAME)](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L6)
- [ ] [**a description**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L16)
- [ ] [**a license**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L68-L75)
- [ ] [**the developers**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L77-L90)
- [ ] [**issueManagement**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L92-L96)
- [ ] [**scm**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L98-L105)
- [ ] [**the ossrhDeploy profile**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L109-L192)
- [ ] [**the githubDeploy profile**](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/605c3ac3f7da571b4d63009a89b0cf22710d1603/pom-example.xml#L195-L206)

*For more details you can look [pom-example.xml](https://github.com/MathieuSoysal/Java-maven-libray-publisher/blob/main/pom-example.xml)*



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
