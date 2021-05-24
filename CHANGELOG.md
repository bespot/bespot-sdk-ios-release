# 0.3.4 (2021-05-24)

### Changed
- Request interval changed to 2.0 seconds (previously 1.0 seconds)

# 0.3.3 (2021-05-17)

### Added
- Extra data added in beacon readings payloads to allow remote signal adjustments for different device types.

# 0.3.2 (2021-04-06)

### Added
- SDK is mapped to production environment (previous: development).
- User identifier can now be provided using `setUserId(_:)` method.

# 0.3.1 (2021-02-26)

### Added
- Store code is now provided as well in InOut status.

### Fixed
- Minor flow crash in case IN-OUT status is explicitly requested without prior IN-OUT status subscription.

# 0.3.0 (2021-02-19)

### Added
- Verified InOut status. Supported status: `IN`, `OUT`, `UNVERIFIED`.  

### Changed
- Location (latitude, longitude) made optional in `subscribeForInOutUpdates` method. InOut updates now can start based on Bluetooth beacon. readings.

### Fixed
- Get InOut status only for the latest distinct EID Bluetooth readings (previously all EID readings were used).

# 0.2.0 (2021-02-07)

### Added
- Get all available stores.
- Last InOut status.
- A list of EIDs provided in `BTInOutStatus` object.

# 0.1.1 (2021-01-08)

### Added
- Initialization configuration singleton with parameters.
- InOut status Subscribe and Unsubscribe methods.
