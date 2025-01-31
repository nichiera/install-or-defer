# Install or Defer Change Log

All notable changes to this project will be documented in this file. This project adheres to [Semantic Versioning](http://semver.org/).


## [Unreleased] - TBD

Nothing yet.

## [2.3.2] - 2019-09-23

### Added

- Added explicit unload of helper LaunchDaemon (fixes an issue where the process persists if the enforced updates do not require a restart, e.g. Safari).

## [2.3.1] - 2019-07-23

### Added

- Added `/usr/bin` to `$PATH` definitions (fixes an issue where third-party Python2 installs fail attempts to read system settings due to missing `Foundation` and `CoreFoundation` modules).

## [2.3.0] - 2019-07-16

### Added

- if a custom software update URL is set, the script now checks that URL for reachability before proceeding


## [2.2.0.1] - 2019-07-15

### Changed

- generalized `$MSG_ACT_OR_DEFER` to refer to "IT" rather than "ExampleCorp" to allow usage of the script or the packaged build without environment-specific modifications


## [2.2] - 2019-06-04

### Added

- added option for custom `$MAX_DEFERRAL_TIME` and `$SKIP_DEFERRAL` settings defined by plist attributes, or if undefined, reverts to script default (allows for managing deferral periods via configuration profile rather than making the change in the script and repackaging)

### Changed

- standardized casing (`UpperCamelCase` for CFPreferences, `ALL_CAPS_WITH_UNDERSCORES` for variables)
- split README text in definition lists into multiple paragraphs


## [2.1.4] - 2019-05-14

### Changed

- added cleanup tasks to preinstall script and `exit_without_updating` (ensures `AppleSoftwareUpdatesForcedAfter` attribute doesn't persist between script reinstalls)
- made `$BUNDLE_ID` LaunchDaemon unload conditional on file existing (reduces error output)


## [2.1.3] - 2019-04-11

### Added

- added `--no-scan` flag to `--download` and `--install` commands (avoids repeatedly checking for updates after initial `softwareupdate --list`, speeding up script runtime)


## [2.1.2] - 2019-04-10

### Added

- added shutdown workflow for BridgeOS updates (detects string  in `softwareupdate --install --all` output indicating a shutdown is required rather than a restart, changes restart function to shut down instead) #10


## [2.1.1] - 2019-04-10

### Changed

- moved update check after deferral period check (reduces amount of `softwareupdate` processes running in the background between deferral periods)
- switched to Software Update icon as default alert branding
- reworded some `echo` output
- consolidated dynamic substitution notes in README
- consistent indent spacing in script


## [2.1] - 2019-01-19

### Added

- added example of a recommended update that doesn't require a restart to README

### Changed

- made system restart conditional on an update requiring it (and made the corresponding messaging variable based on restart requirement)
    - if a restart is required, scripts runs `--all` updates and restarts on completion
    - if a restart is not required, script only runs `--recommended` updates
- consolidated MESSAGING description
- renamed functions and variables to reflect new behaviors
- increased recommended minimum macOS to 10.12+
- formatting changes for consistent spacing and labeling
- switched example smart groups in README to use regex for shorter queries (left old behavior in separate example for older versions of Jamf Pro)
- updated screenshots in README to reflect current script behavior

### Removed

- No longer support 10.11 and earlier


## [2.0] - 2019-01-10

### Added

- added separate `$MSG_UPDATING` alert while updates are running in the background (deferred update during restart not working in 10.13+ #4)
    - gives user option to manually run updates (dynamically describes method of manual updates depending on macOS version)
- added preflight `softwareupdate --list` (more accurate than reading from `/Library/Updates/index.plist`, with tradeoff of longer script runtime #3) before caching updates (script exits if `--list` returns no recommended results)
- added explicit 10.13 and 10.14 support in version checks

### Changed

- set `softwareupdate --download` to only grab `--recommended` updates (as per `README` and the intent of the script to only trigger for security updates requiring restart)
- renamed `trigger_updates_at_restart` to `check_for_updates`, moved recon/unload to dedicated `exit_without_updating` function
- moved updater mechanism to dedicated `run_updates` function
- renamed `clean_up_before_restart` function to `clean_up` (since it isn't always run as part of a restart action)
- changed App Store icon path (.png resource no longer exists in macOS 10.14, and jamfHelper natively supports .icns files)
- updated Casper references to Jamf Pro in `README`
- updated example security patches in `README` to more recent builds (matching naming convention from [Apple security updates](https://support.apple.com/en-us/HT201222))

### Removed

- removed all `/Library/Updates` dependencies as that path is now under SIP in macOS 10.14+


## [1.0.1] - 2017-07-24

### Changed

- specifies full path to helper script #2


## 1.0.0 - 2017-03-02

- Initial release


[Unreleased]: https://github.com/homebysix/install-or-defer/compare/v2.3.2...HEAD
[2.3.2]: https://github.com/homebysix/install-or-defer/compare/v2.3.1...v2.2.3.2
[2.3.1]: https://github.com/homebysix/install-or-defer/compare/v2.3.0...v2.2.3.1
[2.3.0]: https://github.com/homebysix/install-or-defer/compare/v2.2.0.1...v2.2.3.0
[2.2.0.1]: https://github.com/homebysix/install-or-defer/compare/v2.1.4...v2.2.0.1
[2.2]: https://github.com/homebysix/install-or-defer/compare/v2.1.4...v2.2
[2.1.4]: https://github.com/homebysix/install-or-defer/compare/v2.1.3...v2.1.4
[2.1.3]: https://github.com/homebysix/install-or-defer/compare/v2.1.2...v2.1.3
[2.1.2]: https://github.com/homebysix/install-or-defer/compare/v2.1.1...v2.1.2
[2.1.1]: https://github.com/homebysix/install-or-defer/compare/v2.1...v2.1.1
[2.1]: https://github.com/homebysix/install-or-defer/compare/v2.0...v2.1
[2.0]: https://github.com/homebysix/install-or-defer/compare/v1.0.1...v2.0
[1.0.1]: https://github.com/homebysix/install-or-defer/compare/v1.0...v1.0.1
