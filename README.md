
# Rocket.Chat Platform Extension Specification
The purpose of this repository is to define the docker-based [Rocket.Chat](https://rocket.chat/) platform extension specification.

This extention is designed to support team chat.

## Status
 * Support a basic Rocket.Chat load with the mongo backend
 * Currently it can only be accessed directly on port 3000, more nginx work is needed
 * Currently tested in aws instance type
   * Local instance does not seem to work on windows due to docker-compose not being installed in the jenkins container
 * LDAP integration working with manual setup ([see below](#how-to-set-up-ldap-integration-manually))

## To do
 * Complete nginx config file.
 * Get the right hostname (IP) in environment variables during load.
 * Add LDAP configuration during extension load. Currently it must be done manually after the extension is loaded.
 * Investigate if HuBot should be added.

## How to add Rocket.Chat to your platform
1. Run quickstart from [Accenture/adop-docker-compose](https://github.com/Accenture/adop-docker-compose)
 * Use [josequaresma/adop-docker-compose](https://github.com/josequaresma/adop-docker-compose) if you are running it on windows with a username that cointains a dot (".")
2. Go to the [Load Platform configuration](http://YOUR_PLATFORM_IP/jenkins/job/Load_Platform/configure), change the _Branch Specifier_ field to '\*/feature/support-docker-based-platform-extensions' and press _Save_
3. Select _Build with Parameters_ on the left side and use Robert's repo 'https://github.com/RobertNorthard/adop-platform-management.git'
4. Go to the [Load Platform Extension configuration ](http://YOUR_PLATFORM_IP/jenkins/job/Platform_Management/job/Load_Platform_Extension/configure), on the _Execute shell_ code under _Build_ comment out the if block that starts with `if [ ! "${CREDENTIALS}" = "adop-default" ]; then` and press Save
5. Select _Build with Parameters_ on the left side and use the following values:
 * GIT_URL: 'https://github.com/josequaresma/adop-platform-extension-rocket.chat'
 * GIT_REF: convert-to-rocket.chat
 * AWS_CREDENTIALS: 'ADOP LDAP Admin'
6. Rocket.Chat should now be available on [http://YOUR_PLATFORM_IP:3000](http://YOUR_PLATFORM_IP:3000)

## How to set up LDAP integration manually
1. Go to the [login page](http://YOUR_PLATFORM_IP:3000) and register a new account
 * The first user created has admin rights in Rocket.Chat
2. Go to the [LDAP configuration page](http://YOUR_PLATFORM_IP:3000/admin/LDAP) and set the values (the fields not shown here can remain with the default value):
 * Enable: True
 * Host: ldap
 * Port: 389
 * Domain Base: dc=ldap,dc=example,dc=com
 * Domain Search User: cn=admin,dc=ldap,dc=example,dc=com
 * Domain Search Password: YOUR_PLATFORM_LDAP_ADMIN_PASSWORD
 * Domain Search User ID: uid
 * Domain Search Object Class: inetOrgPerson
 * Domain Search Object Category: _EMPTY_
 * Username Field: uid
 * Sync Data: True
 * User Data Field Map: {"displayName":"name", "mail":"email"}
 * Default Domain: _EMPTY_
3. Press _SAVE CHANGES_
4. You should now be able to login using the username and password of a user in LDAP
