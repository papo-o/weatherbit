# Change Log

## [1.0.7] - Unrealeased

### Fixed

- Issue [#56](https://github.com/briis/weatherbit/issues/56) Polish language was falling back to English if HA Locale was not set correctly. Thanks to @andilge for spotting and fixing this.
- Issue [#53](https://github.com/briis/weatherbit/issues/53) Ensure humidity sensor is always reported as integer, without decimals.

## [1.0.6] - 2022-01-05

### Fixed

- **BREAKING CHANGE** [#52](https://github.com/briis/weatherbit/issues/52) Changed Unique ID to use the supplied Latitude and Longitude. The previous value could sometimes change when many stations in close proximity, creating double entries. This unfortunately means that all entities will get a new unique id, and will be duplicated. I recommend to simply delete the Integration and add it again, and all the names should stay the same as before.

- Fixing forecast date not in right format. Date needs to be a UTC time *string* and not DateTime object.


## [1.0.5] - 2021-12-29

### Fixed

- Issue [#50](https://github.com/briis/weatherbit/issues/50) Fixed pressure and visibility values not being correct. **Please note** that when clicking on a weather card, the units for pressure will be reported as `psi` if imperial units or else as `pa`. The values however are in `inHg` and `hPa`. For metric units, wind speed is now also in `m/s` and not `kmh`. Not sure why this was changed on the Weather Entity.


## [1.0.4] - 2021-12-28

### Changed

- Issue [#50](https://github.com/briis/weatherbit/issues/50) Changed the weather entity to use data from the current dataset, so that sensors and the weather entity are in sync on relevant data points.


## [1.0.3] - 2021-12-26

### If you are currently running a version smaller than 1.0.0, then please read the release notes for V1.0.0 before you upgrade

### Added

- New sensor called `observation_time` added. Holds the last update time of the data from the station.


## [1.0.2] - 2021-12-24

### If you are currently running a version smaller than 1.0.0, then please read the release notes for V1.0.0 before you upgrade

### Fixed

- Issue #46. Values for the `forecast_day_X` attributes, were not correct if unit system equals Imperial.

### Changed

- Polish Sensor string updated. Thank you to @nepozs

### Added

- Issue #47. Adding `alt_condition` as attribute to Weather entity. This attribute holds alternative conditions if it is night.


## [1.0.1] - 2021-12-23

### If you are currently running a version smaller than 1.0.0, then please read the release notes for V1.0.0 before you upgrade

### Added

- Issue #43. Added the `forecast_day_X` sensors back as per request. Changed the naming of some of the attributes to be in line with Home Assistant standards.
- Issue #45. City Name is now part of the Attributes for Alerts.

### Changed

- Issue #44. **BREAKING CHANGE** Changed the name of the weather entity to `weather.weatherbit` and the Friendly Name to `Weatherbit` as the previous chosen name was too long. The entity name might stay unchanged, but for some installations it will not, so you might have to update the UI.

### Fixed

- Changed the formula to extract English and Local Language text from the Alerts, to ensure they were in the right order every time.


## [1.0.0] - 2021-12-22

## This release contains breaking changes and you will have to re-define most of your settings in the UI and in automations after installation.

### Upgrade Instructions

Due to the many changes and entities that have been removed and replaced, we recommend the following process to upgrade from an earlier Beta or from an earlier release:

- Upgrade the Integration files, either through HACS (Recommended) or by copying the files manually to your custom_components/weatherbit directory.
- Restart Home Assistant
- Remove the Weatherbit Integration by going to the Integrations page, click the 3 dots in the lower right corner of the Weatherbit Integration and select Delete
- While still on this page, click the + ADD INTEGRATION button in the lower right corner, search for WeatherBit, and start the installation, supplying your credentials.

### Changes

- **BREAKING CHANGE** This is basically a completely new Integration, as all code has been rewritten from the beginning. This goes for the Integration itself, but also for the module `pyweatherbitdata` that this integration uses for communincating with the WeatherBit API. This is done to make the Integration compliant with Home Assistant coding practices and to ensure it is much easier to maintain going forward. As a consequence of that almost all sensors have a new Name and a new Unique ID's, which is why a removal and re-installation is the best option when upgrading to this version. You will also have to change the sensor  and weather entity names in the UI and in Automations that are based on this Integration.
- **Alerts** are now always pulled from Weatherbit, as I found a way to pull that data together with the Current observation data, so it is only 1 call to Weatherbit. If there are no current alerts there will be no Attributes.
- `forecast_day_x` sensors have been removed from the new Integration. Data is already present as attributes in the `weather` entity, but if someone really needs these, please create an issue in Github and I will look at adding them back.
- Fixing Issue #41 and #42. Deprecated `device_state_attributes`.

### Added
- Frontend Translations are now in place for non-standard text based sensors like Beaufort Description, UV Description and Wind Cardinals. This means that the state of the sensor will always be the same, independend of the UI Language, which makes it easier to make automations that go across UI languages. Please see the README file, if you want to translate to your local language.
- Dutch translation for Config Flow added. Thanks to @erik7
- Dutch translation for Sensor UI Values updated. Thanks to @erik7


## [1.0.0-beta.1] - 2021-12-19

This release contains **breaking changes** and you will have to re-define most of your settings in the UI and in automations after installation.

### Upgrade Instructions
Due to the many changes and entities that have been removed and replaced, we recommend the following process to upgrade from an earlier Beta or from an earlier release:

- Upgrade the Integration files, either through HACS (Recommended) or by copying the files manually to your custom_components/weatherbit directory.
- Restart Home Assistant
- Remove the Weatherbit Integration by going to the Integrations page, click the 3 dots in the lower right corner of the Weatherbit Integration and select Delete
- While still on this page, click the + ADD INTEGRATION button in the lower right corner, search for WeatherBit, and start the installation, supplying your credentials.

### Changes
- **BREAKING CHANGE** This is basically a completely new Integration, as all code has been rewritten from the beginning. This goes for the Integration itself, but also for the module `pyweatherbitdata` that this integration uses for communincating with the WeatherBit API. This is done to make the Integration compliant with Home Assistant coding practices and to ensure it is much easier to maintain going forward. As a consequence of that almost all sensors have a new Name and a new Unique ID's, which is why a removal and re-installation is the best option when upgrading to this version. You will also have to change the sensor  and weather entity names in the UI and in Automations that are based on this Integration.
- **Alerts** are now always pulled from Weatherbit, as I found a way to pull that data together with the Current observation data, so it is only 1 call to Weatherbit. If there are no current alerts there will be no Attributes.
- `forecast_day_x` sensors have been removed from the new Integration. Data is already present as attributes in the `weather` entity, but if someone really needs these, please create an issue in Github and I will look at adding them back.
- Fixing Issue #41 and #42. Deprecated `device_state_attributes`.

### Added
- Frontend Translations are now in place for non-standard text based sensors like Beaufort Description, UV Description and Wind Cardinals. This means that the state of the sensor will always be the same, independend of the UI Language, which makes it easier to make automations that go across UI languages. Please see the README file, if you want to translate to your local language.

