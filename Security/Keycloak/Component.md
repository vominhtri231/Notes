# Components

## Realm

A Realm manges a set of users, credentials, roles, groups.  
There are 2 types of realms:

* Master realm: contains the admin account, use this to create other realms only.
* Other realms

## Client

Clients are applications or services that can ask Keycloak to authenticate a user.  
User can login to a specific client by:
`{keycloak-server}/auth/realms/{realm}/protocol/openid-connect/auth?response_type=code&client_id={client-id}`
