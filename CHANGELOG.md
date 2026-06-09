# Changelog

All notable changes to the [Sigmyne/redisx](https://github.com/Sigmyne/redisx) library will be 
documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to 
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [1.0.4-rc3] - 2026-05-31

Upcoming maintenance release, expected between 1 July and 1 August 2026.

### Fixed

 - #29: Occasional segfaults when link is shut down.
 
 - #35: Fixed `redisxPrintDelimited()` for attribute RESP type.
 
 - Fixed deadlock in `redisxGetAvailable()`.
 
 - Fix potential buffer overflow at build time in `docedit.c` (changed `sprintf()` to `snprintf()`).
 
 - `redisxSelectDB()` to store updated DB index (it did not before).
 
 - Fixed thread-safe disconnect procedure to avoid occasional deadlocks and race conditions.

 - CMake `redisxConfig` to skip requiring math lib for non-Windows platforms in general, since it can fail if the 
   math library is in the build path, but not in the search path, such as for some cross builds (see e.g. the vcpkg 
   Android builds)
 
 - Various smaller fixes to issues spotted by Copilot AI.
 
### Added

 - #30: Added CMake build configuration and CI workflows.
 
### Changed

 - #31: Portability to Windows / MSC.
 
 - #33: More efficient reading of large string data, by skipping intermediate buffer when not necessary. 
 
 - #34: Use `snprintf()` instead of `sprintf()` provided it's available. (On older platforms prior to the C99 
   standard, it defaults to `sprintf()`.)
 
 - Removed superfluous (and potentially problematic) error check in `rReadToken()`.

 - `examples/Makefile` to work standalone, without `config.mk`.


## [1.0.3] - 2026-02-16

Maintenance release.

### Fixed

 - #26: `redisxDisconnect()` did not close subscription client.
 
### Changed

 - Disconnecting a Redis instance now shuts down reads on its clients immediately, ensuring that we don't wait
   forever on blocked reads.
   
 - No incomplete array warnings from disabled (closed) clients.
 

## [1.0.2] - 2025-11-17

Maintenance release.

### Changed

 - #13: Replaced deprecated `inet_addr()` and `inet_ntoa()` functions with more modern equivalents, which support IPv6
   also.
   

## [1.0.1] - 2025-08-01

Bug fix release.

### Fixed

 - IPv6 host name resolution.

### Changed

 - Sockets are now always initialized with `SO_LINGER` disabled. Previously that was the case only when a timeout 
   value was configured.

 - More consistent distinction between debug messages (i.e. error traces), verbose output, and warning messages.


## [1.0.0] - 2025-05-06

Initial public release.
