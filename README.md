# Amazon Web Services SDK 2 Plugin

This plugin provides the [AWS SDK for Java](https://aws.amazon.com/sdk-for-java/) as a library to be used by other plugins. It follows the same versioning as the AWS SDK itself.

## Plugins

### `aws-java-sdk2-core`

This plugin contains shared libraries for use by AWS Java SDK modules.
This plugin also contains the STS AWS Java SDK module, because shared authentication libraries need it in the same classpath and the structured classloaders in Jenkins do not permit the use of a separate plugin.

* aws-java-sdk-sts

### `aws-java-sdk2-*`

Contains an individual AWS Java SDK module with the same name.

## Adding a new plugin

If you need to use an AWS Java SDK module that is not yet published as its own plugin, feel free to submit a pull request to create a plugin for it.

* Create a new directory `aws-java-sdk2-<name>`. The name should be identical to the AWS Java SDK module.
* Create `pom.xml`.
  * Depend on `software.amazon.awssdk:<name>`. Exclude all transitive dependencies.
  * Transitive dependencies should be replaced by their equivalent plugin dependency. Most AWS Java SDK modules only depend on the shared libraries in the `aws-java-sdk2-core` plugin. If `aws-java-sdk2-core` is missing a shared library, feel free to add it.
* Create `src/main/resource/index.jelly`. Look at existing modules and adapt it.
* Add the module to the root `pom.xml`.
