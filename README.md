# Wren Security Parent

[![License](https://img.shields.io/badge/license-CDDL-blue.svg)](https://github.com/WrenSecurity/wrenidm/blob/master/LICENSE)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/WrenSecurity)

Parent POM for Wren Security projects provides default plugin definition and project build configuration.


## Conventions

When updating the POM keep in mind following conventions:

* all plugins **MUST** be defined using explicit version to make builds reproducible (i.e. no version ranges)
* all plugins **MUST** have full coordinates inside `<pluginManagement>` section (i.e. no loose plugin references from `<profiles>` section)
* plugin version **SHOULD** be defined using maven property to allow simple version override
* plugin definitions inside the POM are sorted alphabetically by artifact ID
* plugin definitions can contain [processing instructions for m2e lifecycle](http://www.eclipse.org/m2e/documentation/release-notes-17.html#new-syntax-for-specifying-lifecycle-mapping-metadata)
* plugin artifact signatures are verified during the build so make sure all the [keys are trusted](https://github.com/WrenSecurity/wrensec-pgp-whitelist/)


## Plugin Specifics

TODO document important (worth mentioning) plugin configuration


## Profile Specifics

Available profiles:

* `enforce` - runs Maven Enforcer Plugin (active by default)
* `precommit` - runs Maven Checkstyle Plugin
* `metrics` - runs various project reporting plugins (FindBugs, Cobertura, PMD)
* `full-release` - creates and attaches javadoc and source JARs as project artifacts
* `verify-artifact-sigs` - verifies artifacti signatures (active by default)
* `clirr` - TODO document


## Housekeeping (useful for child project)

Show available version updates:

    mvn versions:display-plugin-updates
    mvn versions:display-dependency-updates
    mvn versions:use-latest-versions

Dependency version check (useful when updating):

    mvn dependency:resolve -DoutputFile=dependencies.txt
    mvn dependency:resolve-plugins -DoutputFile=plugin-dependencies.txt

OSGi version check (useful when updating):

    bnd print -Cci target/*.jar
