# Black Duck CoPilot Scala Build Tool/Circle CI Example

[![CircleCI](https://img.shields.io/circleci/project/github/BlackDuckCoPilot/example-sbt-circle/master.svg)](https://circleci.com/gh/BlackDuckCoPilot/example-sbt-circle) [![Black Duck Security Risk](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-sbt-circle/public/results/branches/master/badge-risk.svg)](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-sbt-circle/public/results/branches/master)

Shows a working setup for using the Black Duck CoPilot integration to analyze the risk of project dependencies

## Scala Build Tool Setup
The `project/plugins.sbt` file has been modified to use the [hub-sbt-plugin](https://github.com/blackducksoftware/hub-sbt-plugin) to generate the data used by CoPilot for analysis:

```scala
addSbtPlugin("com.blackducksoftware.integration" % "hub-sbt-plugin" % "1.1.0")
```

## Circle CI Setup

The `circle.yml` file has been modified to upload the generated data to Black Duck CoPilot:

```yaml
test:
  post:
    - sbt -DdeployHubBdio=false buildBom
    - bash <(curl -s https://copilot.blackducksoftware.com/bash/circle) ./target/blackduck/*_bdio.jsonld
```
