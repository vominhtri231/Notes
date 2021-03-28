Clients are applications or services that can ask Keycloak to authenticate a user. 

User can login to a specific client by:
`{keycloak-server}/auth/realms/{realm}/protocol/openid-connect/auth?response_type=code&client_id={client-id}`
