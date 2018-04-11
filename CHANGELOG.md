# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased & outstanding issues]
- Non-https repo url and apt fetching
- APM errors around log location

## [1.2.0] - 2018-04-11
Changed buildpack to use dyno hostnames rather than setting the application name as the hostname. Though the previous method helped simplify continuity, it led to metrics aggregation errors for applications running many dynos. The application name is now available under the "appname" tag when Heroku Labs Dyno Metadata is enabled or the "HEROKU_APP_NAME" environment variable is set.

### Changed
- Hostname will default to dyno host name, unless DD_HOSTNAME is set (not recommended)

### Added
- Application name added as "appname" tag.

### Removed
- Removed README documentation about histogram percentiles and APM that were not specific to the buildpack. See https://docs.datadoghq.com for information about those features.

## [1.1.0] - 2018-03-15
Start the Trace Agent.

### Changed
- Removed Trace Agent config file code. The Trace Agent now uses the main datadog.yaml file.
- Updated the README file to document DD_APM_ENABLED.

### Added
- Datadog Agent 6 no longer starts the Trace Agent (was moved to systemd service for Linux systems). Added code to start the Trace Agent.

## [1.0.1] - 2018-03-02
Resolved issue with dpkg and multiple packages available

### Changed
- Includes a fix from Zunda that limits the dpkg install to the latest package.

## [1.0.0] - 2018-02-28
Updated the buildpack to use stable releases and removed alpha flag (because nobody really knows what that means anyway ;))

### Changed
- Updated the apt repo to use `stable 6` (no longer beta)
- Incorporates a parameter change that resolved problems in beta rc releases (Thanks Zunda!)

## [1.0.0-alpha2] - 2018-02-05
Mostly fixes and a small feature.

### Added
- If no Datadog Agent version has been pinned, the build process will tell you how to pin the current version.

### Changed
- Updated the runner script to insert tags in the correct location in the conf file.
- Env vars are not automatically loaded when building slugs, so the previous version pinning didn't work.

## [1.0.0-alpha1] - 2017-11-21
The buildpack was re-written to use the new Datadog Agent 6 and gather full system metrics.

### Added
- Added an Apache 2 license.
- Added a notice file with copyright info.
- Added a way to pin Datadog Agent versions.
- Added a changelog.
- Added a more comprehensive "Contributing" section to the readme.

### Changed
- Updated from the Datadag Agent 5 to Agent 6. This includes the main agent and the trace agent.

### Removed
- Deprecated env vars that no longer apply in Agent 6

## [legacy] - 2017-11-21
Note that the previous Agent-5-based version of the buildpack is now available using the `legacy` tag.
To continue using this old version, you can update your app by running:
```shell
# Remove the old untagged buildpack
heroku buildpacks:remove https://github.com/DataDog/heroku-buildpack-datadog.git
# Add the tagged version of the buildpack
heroku buildpacks:add --index 1 https://github.com/DataDog/heroku-buildpack-datadog.git#legacy
```
