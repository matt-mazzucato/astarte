# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- Add astarte_import tool, which allows users to import devices and data using XML files.
- [appegnine_api] Add new `/v1/socket` route for Astarte Channels. The `/socket` route is **deprecated** and will be
  removed in a future release.
- [appengine_api] Add groups support, allowing to group devices and access them inside a group hierarchy.
- [appengine_api] Add Prometheus metrics.
- [appengine_api] Show interface stats (exchanged messages and bytes) in device introspection.
- [appengine_api] Add previous_interfaces field to device details.
- [appengine_api] Allow installing group triggers in Astarte Channels.
- [data_updater_plant] Add support to multiple queues with consistent hashing
- [data_updater_plant] Save exchanged bytes and messages for all interfaces.
- [housekeeping] Add groups related columns and tables (schema has been changed).
- [housekeeping] Add interface stats related columns (schema has been changed).
- [housekeeping] Add database retention ttl and policy related columns (schema has been changed).
- Allow specifying initial introspection when registering a device.
- [realm_management] Trigger validation, checks that the interface is existing and performs validation on object aggregation triggers.

### Changed
- Use separate docker images with docker-compose
- Use Scylla instead of Cassandra with docker-compose
- Authorization regular expressions must not have delimiters: they are implicit.
- [appengine_api] Change logs format to logfmt.
- [data_updater_plant] Changed logs format to logfmt.
- [realm_management] Changed logs format to logfmt.
- [realm_management_api] Changed logs format to logfmt.
- [housekeeping] Change database driver, start using Xandra.
- [housekeeping_api] Move health check API from /v1/health to /health to be consistent with all Astarte components.

## [0.10.2] - 2019-12-09
### Added
- [appengine_api] Add timestamp field to channel events.
- Add device unregister API, allowing to reset the registration of a device.

### Fixed
- [appengine_api] Fix invalid dates handling, they should not cause an internal server error.
- [appengine_api] Gracefully handle existing aliases instead of returning an internal server error.
- [appengine_api] Fix querying object aggregated interface with explicit timestamp, use value_timestamp to avoid
an internal server error.
- [appengine_api] Device details now show false in the connected field for never connected devices (null was
  returned before)
- [appengine_api] Handle out-of-band RPC errors gracefully instead of crashing.
- [data_updater_plant] Do not accept invalid paths that have consecutive slashes.
- [data_updater_plant] Do not accept invalid paths in object aggregated interfaces.
- [data_updater_plant] Do not delete all congruent triggers when deleting a volatile trigger.
- [data_updater_plant] Load volatile device triggers as soon as they're installed.
- [realm_management_api] Handle trigger not found reply from RPC, return 404 instead of 500.

### Changed
- Use the timestamp sent by VerneMQ (or explicit timestamp if available) to populate SimpleEvent timestamp.
- [data_updater_plant] Update suggested RabbitMQ version to 3.7.15, older versions can be still used.

## [0.10.1] - 2019-10-02
### Added
- Support both SimpleStrategy and NetworkTopologyStrategy replications when creating a realm.
- Add sanity checks on the replication factor during realm creation.

### Fixed
- Auth was refusing any POST method, a workaround has been added, however this will not work with regex.
- Fix reversed order when sending binaryblobarray and datetimearray.
- [data_updater_plant] Fix a bug that was causing a crash-loop in some corner cases when a message was sent on an outdated interface.
- [data_updater_plant] Send consumer properties correctly when handling `emptyCache` control message.
- Use updated interface validation: object aggregated properties interfaces are not valid.
- Use updated interface validation: server owned object aggregated interfaces are not yet supported, hence not valid.
- [realm_management_api] Trying to create a trigger with an already taken name now fails gracefully with an error instead of crashing.
- [trigger_engine] Fix datetime type handling, now it is properly serialized.

## [0.10.0] - 2019-04-16

## [0.10.0-rc.0] - 2019-04-03
### Added
- [data_updater_plant] Add missing support to incoming object aggregated data with explicit_timestamp.

## [0.10.0-beta.3] - 2018-12-19
### Added
- [appengine_api] Binary blobs and date time values handling when PUTing and POSTing on a server owned interface.

### Fixed
- docker-compose: Ensure CFSSL persists the CA when no external CA is provided.
- [data_updater_plant] Correctly handle Bson.UTC and Bson.Bin incoming data.
- [data_updater_plant] Fix crash when an interface that has been previously removed from the device introspection expires from cache.
- [data_updater_plant] Undecodable BSON payloads handling (handle Bson.Decoder.Error struct).
- [data_updater_plant] Discard invalid introspection payloads instead of crashing the data updater process.
- [realm_management_api] Correctly serialize triggers on the special "*" interface and device.

## [0.10.0-beta.2] - 2018-10-19
### Added
- Automatically add begin and end delimiters to authorization regular expressions.
- [appengine_api] Value type and size validation.
- [appengine_api] Option to enable HTTP compression.
- [data_updater_plant] Allow to expire old data using Cassandra TTL.
- [data_updater_plant] Publish set properties list to `/control/consumer/properties`.

### Fixed
- [appengine_api] Path was added twice in authorization path, resulting in failures in authorization.
- [appengine_api] POST to a datastream endpoint doesn't crash anymore.
- [data_updater_plant] Validate all incoming values before performing any further computation on them, to avoid crash loops.
- [data_updater_plant] Fix a bug preventing data triggers to be correctly loaded
- [realm_management] Interface update, it was applying a broken update.
- [realm_management_api] Do not reply "Internal Server Error" when trying to delete a non existing interface.

### Changed
- [appengine_api] "data" key is used instead of "value" when PUT/POSTing a value to an interface.
- [appengine_api] APPENGINE_MAX_RESULTS_LIMIT env var was renamed to APPENGINE_API_MAX_RESULTS_LIMIT.

## [0.10.0-beta.1] - 2018-08-10
### Added
- First Astarte release.
