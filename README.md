# Black Duck CoPilot Scala Build Tool/Travis CI Example

[![Travis CI](https://travis-ci.org/BlackDuckCoPilot/example-sbt-travis.svg?branch=master)](https://travis-ci.org/BlackDuckCoPilot/example-sbt-travis) [![Black Duck Security Risk](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-sbt-travis/public/results/branches/master/badge-risk.svg)](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-sbt-travis/public/results/branches/master)

Shows a working setup for using the Black Duck CoPilot integration to analyze the risk of project dependencies

## Scala Build Tool Setup
The `project/plugins.sbt` file has been modified to use the [hub-sbt-plugin](https://github.com/blackducksoftware/hub-sbt-plugin) to generate the data used by CoPilot for analysis:

```scala
addSbtPlugin("com.blackducksoftware.integration" % "hub-sbt-plugin" % "1.1.0")
```

## Travis CI Setup

The `.travis.yml` file has been modified to upload the generated data to Black Duck CoPilot:

```yaml
after_success:
- sbt -DdeployHubBdio=false buildBom
- bash <(curl -s https://copilot.blackducksoftware.com/bash/travis) ./target/blackduck/*_bdio.jsonld
```
