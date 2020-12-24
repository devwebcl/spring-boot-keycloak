## Spring Boot Keycloak

https://www.baeldung.com/spring-boot-keycloak


- http://localhost:8081/



unzip keycloak-11.0.2.zip
cd keycloak-11.0.2/bin
./standalone.sh -Djboss.socket.binding.port-offset=100

- Despues de instalar keycloak y configurar realm, client, user.

- hay que ejecutar

Now let's open a browser and visit Keycloak: http://localhost:8180. We'll be redirected to http://localhost:8180/auth to create an administrative login:



This module contains articles about Keycloak in Spring Boot projects.


Keycloak provides a REST API for generating and refreshing access tokens. We can easily use this API to create our own login page.

First, we need to acquire an access token from Keycloak by sending a POST request to this URL:

http://localhost:8180/auth/realms/master/protocol/openid-connect/token

The request should have this JSON body:

{
    'client_id': 'your_client_id',
    'username': 'your_username',
    'password': 'your_password',
    'grant_type': 'password'
}

In response, we'll get an access_token and a refresh_token.

The access token should be used in every request to a Keycloak-protected resource by simply placing it in the Authorization header:

headers: {
    'Authorization': 'Bearer' + access_token
}

Once the access token has expired, we can refresh it by sending a POST request to the same URL as above, but containing the refresh token instead of username and password:

{
    'client_id': 'your_client_id',
    'refresh_token': refresh_token_from_previous_request,
    'grant_type': 'refresh_token'
}

Keycloak will respond to this with a new access_token and refresh_token.


## Relevant articles:
- [A Quick Guide to Using Keycloak with Spring Boot](https://www.baeldung.com/spring-boot-keycloak)
- [Custom User Attributes with Keycloak](https://www.baeldung.com/keycloak-custom-user-attributes)
- [Customizing the Login Page for Keycloak](https://www.baeldung.com/keycloak-custom-login-page)
- [Keycloak User Self-Registration](https://www.baeldung.com/keycloak-user-registration)
- [Customizing Themes for Keycloak](https://www.baeldung.com/spring-keycloak-custom-themes)

