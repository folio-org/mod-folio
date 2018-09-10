# mod-rmb-template

Copyright (C) 2017-2018 The Open Library Foundation

This software is distributed under the terms of the Apache License, Version 2.0.
See the file "[LICENSE](LICENSE)" for more information.

## Introduction

This is a Maven archetype used to generate an RMB-based server-side module. Install this locally if you wish to build such a module.

RAML Module Builder (or RMB) is a Vert.x based toolkit that enables a module to:
* synthesize API endpoints (via a Java interface) based on a RAML document
* synthesize POJOs based on declared JSON schema definitions
* take advantage of other abstraction

For additional information on RMB, please refer to the [README](https://github.com/folio-org/raml-module-builder).

See other initial module setup [guidelines](https://dev.folio.org/guidelines/create-new-repo)
and [naming conventions](https://dev.folio.org/guidelines/naming-conventions/),
and the guide [Commence a module - structure and configuration](https://dev.folio.org/guides/commence-a-module/).

## Usage

First, build and install this mod-rmb-template facility locally:

```
mvn clean install
```

On success, go to the root that will host your new project folder and run the following command.
For the `artifactId` follow the `mod-` prefix naming convention.

```
mvn archetype:generate \
  -DarchetypeGroupId=org.folio \
  -DarchetypeArtifactId=mod-rmb-template \
  -DarchetypeVersion=1.1.0-SNAPSHOT \
  -DgroupId=org.folio \
  -Dversion=1.0.1-SNAPSHOT \
  -DartifactId={project-module-name-here}
```

Do `cd` into the new project's directory.

```
git init
```

Add the [raml-util](https://github.com/folio-org/raml) which provides resources shared by RAML-based FOLIO modules.
**NOTE**: 20180910: use its "raml1.0" branch:

```
git submodule add https://github.com/folio-org/raml ramls/raml-util
cd ramls/raml-util
git checkout raml1.0
cd ../..
git add ramls/raml-util
```

At this point, the new module is ready for initial compilation.

`mvn clean install`

> NOTE: Once compiled, this new project will not have an actual API implementation. The Java interface files would have been generated into `target/generated-sources/raml-jaxrs` based on the provided RAML and Schema files.

## Next steps

Follow the RMB [README](https://github.com/folio-org/raml-module-builder) to understand how it works.

Compare the files that were generated by this archetype with that explained in the RMB README and in the exemplar modules (mod-tags, mod-notify, and mod-notes) especially `pom.xml` and `descriptors/ModuleDescriptor-template.json` files.

Replace the basic RAML and schema files with ones to suit your project. Follow the RMB [advice](https://github.com/folio-org/raml-module-builder/blob/master/README.md#step-6-design-the-raml-files) and investigate other modules.

Commence your API implementation:
```
src/main/java/org/folio/rest/impl/PetsResourceImpl.java
src/test/java/org/folio/rest/impl/PetsTest.java
```

