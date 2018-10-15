# Keycloak dynamic branding

In Keycloak, URI information is not passed by default to FTL templates, thus making it hard to implement dynamic theme branding. However, it's easy to push any arbitrary data, including URI info, to FTL context using Keycloak providers mechanism.

This example demonstrates this approach with dynamically branded login theme.

## Build
```
mvn clean install
```

## Install
```
cp */target/*.jar $KEYCLOAK/standalone/deployments
```

## Configure

In `standalone.xml` (server/profile/subsystem[@xmlns="urn:jboss:domain:keycloak-server:1.1"]):
```
            <spi name="login">
                <default-provider>freemarker+</default-provider>
                <provider name="freemarker+" enabled="true"/>
            </spi>
```

In Admin Console: realm settings → Themes → Login Theme = glutt

# Test

Try appending "glutt" parameter either to client URL or to Keycloak auth URL. For example:

`http://localhost:8080/auth/admin/master/console?glutt=1`

`http://localhost:8080/auth/realms/master/protocol/openid-connect/auth?client_id=security-admin-console&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2Fauth%2Fadmin%2Fmaster%2Fconsole%2F&response_mode=fragment&response_type=code&scope=openid&glutt=1`

This should change Keycloak logo to that of The World's Leading Glutt Producer™.
