# Maven Central publishing

The project uses the `io.github.jcondotta` namespace and MIT license. The first
release candidate is `0.1.0-alpha.1`. Do not reuse this version after publication;
Maven Central releases are immutable.

## Local prerequisites

Install GnuPG and create a signing key following
[Sonatype's GPG guide](https://central.sonatype.org/publish/requirements/gpg/).
Publish the public key to a keyserver and register the signing key in the Central
Portal. Keep the private key and passphrase private; neither belongs in this repo.

Create a Central Portal user token. Copy `.mvn/settings.example.xml` to the ignored
`.mvn/settings.xml`, replacing the placeholders with the token username and password.
Maven does not automatically load project-local settings, so pass
`-s .mvn/settings.xml` to commands that need the credentials. Do not commit this file.

## Build and inspect

Run the full test suite and build source and Javadoc artifacts without signing:

```sh
mvn -Prelease clean verify -Dgpg.skip=true
```

Inspect the POM metadata and `target/domain-core-0.1.0-alpha.1-sources.jar` plus
`target/domain-core-0.1.0-alpha.1-javadoc.jar`. Then create and sign a local bundle
without uploading it:

```sh
mvn -Prelease clean deploy -DskipUpload=true
```

This produces `target/central-publishing/central-bundle.zip`. Review the bundle before
submitting it through the Central Portal. The signing step requires the local GPG key;
creating the bundle this way does not require Portal credentials.

## Submit and publish

After reviewing the bundle and configuring both GPG and the Portal token, submit it for
validation:

```sh
mvn -s .mvn/settings.xml -Prelease clean deploy
```

The POM sets `autoPublish` to `false`, so successful validation does not publish the
artifact automatically. Review and publish the deployment in the Central Portal. Then
verify `io.github.jcondotta:domain-core:0.1.0-alpha.1` from a separate consumer project
using an empty local Maven repository.

After publication, tag the release source as `v0.1.0-alpha.1` and change the POM and
README dependency example to the next development version, `0.1.0-alpha.2-SNAPSHOT`.
