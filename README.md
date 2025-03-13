# Amazon Web Services SDK 2 Plugin

This plugin provides the [AWS SDK for Java](https://aws.amazon.com/sdk-for-java/) as a library to be used by other plugins. It follows the same versioning as the AWS SDK itself.

## Requesting new instance types

Some plugins rely on the AWS SDK to list available instance types. Updates of the AWS SDK come via this plugin.

There is a regular release of the AWS SDK, and most updates are not relevant to most Jenkins users.

As the current maintainer of this library plugin, I am not actively monitoring the [AWS SDK changelog](https://github.com/aws/aws-sdk-java/blob/master/CHANGELOG.md/).

To use a new instance type that is not yet available through this plugin:

* Look up the version of AWS SDK that it was introduced ([changelog](https://github.com/aws/aws-sdk-java-v2/blob/master/CHANGELOG.md))
* Find the latest dependabot pull request bumping the AWS SDK ([link](https://github.com/jenkinsci/aws-java-sdk2-plugin/pulls?q=is:pr+is:open+sort:updated-desc+revision/))
* Ask for a merge and release and the version of the AWS SDK it was introduced in, after providing the instance type you are looking for.

## Plugins

### `aws-java-sdk2-core`

This plugin contains shared libraries for use by AWS Java SDK modules.
This plugin also contains the STS AWS Java SDK module, because shared authentication libraries need it in the same classpath and the structured classloaders in Jenkins do not permit the use of a separate plugin.

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
