
# Rocket.Chat Platform Extension Specification
The purpose of this repository is to define the docker-based [Rocket.Chat](https://rocket.chat/) platform extension specification.

This extention is designed to support team chat.

## Status
 * Support a basic Rocet.Chat load with the mongo backend
 * Currently it can only be accessed directly on port 3000, more nginx work is needed
 * ...

### To do 
 * Test manual LDAP config 
 * Complete nginx config file.
 * Get the right hostname (IP) in environment variables during load.
 * Add LDAP configuration during extension load. Currently it must be done manually after the extension is loaded.
 * Investigate if HuBot should be added. 

## Stucture
A platform specification is broken down into the following sections:

 * service
  * This is to add more services to the platform.

## Metadata
Each cartridge should contain a "extension.metadata" file that specifies the following metadata:

 * `PLATFORM_EXTENSION_SDK_VERSION`
  * This defines the version of the Cartridge SDK that the cartridge conforms to
 * `PLATFORM_EXTENSION_NAME`
  * This is the name of the platform extension which should reflect the purpose of the extension.
 * `PLATFORM_EXTENSION_TYPE`
  * This is the type of platform extension.
