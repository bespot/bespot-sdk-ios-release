# 0.6.0 (2024-12-04)

### Added
- Support Xcode 16.1 and Swift 6
- Surveys feature

# 0.5.1 (2024-01-19)

### Added
- Promote `Service unavailable outside business hours` error

# 0.5.0 (2023-12-1)

### Changed
- Rename `BespotSDK` class to `BTSDK`

### Added
- Support XCFramework

# 0.4.11 (2023-09-26)

### Added
- Support for Swift 5.9

### Changed
- Support for iOS 12+

# 0.4.10 (2023-08-04)

### Added
- Complete BespotSDK initialisation (authenticate with server) when network is not available initially but becomes available later on.

# 0.4.9 (2023-07-12)

### Added
- Support for Swift 5.8.1

# 0.4.8 (2023-06-28)

### Added
- Expose `setAltUserId(_:)` function for setting an alternative user ID

# 0.4.7 (2023-04-05)

### Added
- SDK: Support swift 5.8

# 0.4.6 (2022-11-11)

### Added
- SDK: Support swift 5.7.1

# 0.4.5 (2022-10-27)

### Added
- iBeacon scanning capability added (introduced `BTiBeaconScanner` class)

### Changed  
- Variables (distance, rssi, txPower, UUID, major, minor, profileType) of `BTReading` class made publicly accessible

# 0.4.4 (2022-05-18)

### Changed
- Updated LICENCE information under README.md


# 0.4.3 (2022-04-08)

### Fixed
- Exposed `BTError` properties - made them public

# 0.4.2 (2022-02-24)

### Changed
- apiError -> unknownServerError
- Timestamp changed from seconds to milliseconds
- Refactoring of the startScanning and didUpdateBeacon methods (INTERNAL)

### Added
- BTConfigurationDelegate protocol with didCompleteConfiguration(), didFailUpdateConfiguration(error: BTError) methods added
- New errors: See BTErrorType enum
- Interruption of the InOut flow if authentication (successful configuration) has not been completed
- Error propagation (.networkError) due to decoding failure in the InOut status

### Fixed
- Bug with InOut updates stop being delivered in case of network being recovered (network previously disabled or unavailable)
- Bug of sending misleading AWAY status when no network is available

### Removed
- [BREAKING] .unverified case removed from BTInOutStatusType enumeration

# 0.4.1 (2022-01-25)

### Added
- SDK: Xcode 13 support

# 0.4.0 (2021-10-19)

### Changed
- Logger time changed to 24h format
- AWAY status returned instead of OUT in case of no bluetooth readings reception when subscribed (every 5 seconds)

### Added
 - Expose internal session configuration values to the server (through the `metadata` field) (internal)

### Fixed
- Only EID packets are now used. Other packets (such as EDDYSTONE UID) are now filtered out.
- Bluetooth scanning refresh to avoid decreased beacon readings number over time.

# 0.3.6 (2021-06-10)

### Changed
- Return `nil` store code in case of no bluetooth readings reception (OUT status, `nil` EIDs).

# 0.3.5 (2021-05-28)

### Added
- SDK: In case of no bluetooth readings reception when subscribed, send client side OUT every 5 seconds.

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
