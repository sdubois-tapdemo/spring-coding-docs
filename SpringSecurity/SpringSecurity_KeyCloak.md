# SpringDataJPA - Employee JPA/RestAPI Example with JpaRepository

## JPA Project Setup
```
project
  |__ pom.xml
  |__ src
  |    |__ main
  |    |    |__ java
  |    |    |      |__ com.tanzu.KeycloakApp
  |    |    |           |__ KeycloakAppApplication.java        // Application Properties
  |    |    |           |__ controller                        
  |    |    |           |     |__ ControllerHello.java         // Data Access Object (DOA) Interface - JPA Reposity
  |    |    |           |__ security                      
  |    |    |                 |__ JwtConverter.java            // Employee Service Interface
  |    |    |                 |__ JwtConverterProperties.java  // Employee Service implementation 
  |    |    |__ resources
  |    |           |__ application.properties                  // Application Properties
  |    |           |__ static                                  // HTML Files, CSS, JavaScript, imges, etc.
  |    |           |__ templates                               // Auto Configuration Templates (Mustache, FreeMarker, Thymeleaf)
  |    |
  |    |__ test
  |         |__ java
  |
  |__ target

```

## Application Properties
```
server.port=8081

spring.application.name=KeycloakSpringBootApplication
# Security Configuration
spring.security.oauth2.resourceserver.jwt.issuer-uri=https://keycloak.apps.tapmc.tanzudemohub.com/realms/SpringBootKeycloak
spring.security.oauth2.resourceserver.jwt.jwk-set-uri=${spring.security.oauth2.resourceserver.jwt.issuer-uri}/protocol/openid-connect/certs

# JWT Configuration
jwt.auth.converter.resource-id=keycloak-app
jwt.auth.converter.principal-attribute=principal_username

# Logging Configuration
logging.level.org.springframework.security=DEBUG
```

## Security Package
### JWT Converter Class (JwtConverter.java)
```
package com.KeycloakApp.KeycloakApp.security;

import org.springframework.core.convert.converter.Converter;
import org.springframework.security.authentication.AbstractAuthenticationToken;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.oauth2.jwt.Jwt;
import org.springframework.security.oauth2.jwt.JwtClaimNames;
import org.springframework.security.oauth2.server.resource.authentication.JwtAuthenticationToken;
import org.springframework.security.oauth2.server.resource.authentication.JwtGrantedAuthoritiesConverter;
import org.springframework.stereotype.Component;

import java.util.Collection;
import java.util.Map;
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.Stream;

@Component
public class JwtConverter implements Converter<Jwt, AbstractAuthenticationToken> {

    private final JwtGrantedAuthoritiesConverter jwtGrantedAuthoritiesConverter = new JwtGrantedAuthoritiesConverter();

    private final JwtConverterProperties properties;

    public JwtConverter(JwtConverterProperties properties) {
        this.properties = properties;
    }

    @Override
    public AbstractAuthenticationToken convert(Jwt jwt) {
        Collection<GrantedAuthority> authorities = Stream.concat(
                jwtGrantedAuthoritiesConverter.convert(jwt).stream(),
                extractResourceRoles(jwt).stream()).collect(Collectors.toSet());
        return new JwtAuthenticationToken(jwt, authorities, getPrincipalClaimName(jwt));
    }

    private String getPrincipalClaimName(Jwt jwt) {
        String claimName = JwtClaimNames.SUB;
        if (properties.getPrincipalAttribute() != null) {
            claimName = properties.getPrincipalAttribute();
        }
        return jwt.getClaim(claimName);
    }

    private Collection<? extends GrantedAuthority> extractResourceRoles(Jwt jwt) {
        Map<String, Object> resourceAccess = jwt.getClaim("resource_access");
        Map<String, Object> resource;
        Collection<String> resourceRoles;

        if (resourceAccess == null
                || (resource = (Map<String, Object>) resourceAccess.get(properties.getResourceId())) == null
                || (resourceRoles = (Collection<String>) resource.get("roles")) == null) {
            return Set.of();
        }
        return resourceRoles.stream()
                .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
                .collect(Collectors.toSet());
    }
}
```

### JWT Converter Properties Class (JwtConverterProperties.java)
```
package com.KeycloakApp.KeycloakApp.security;

import lombok.Data;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Configuration;
import org.springframework.validation.annotation.Validated;

@Data
@Validated
@Configuration
@ConfigurationProperties(prefix = "jwt.auth.converter")
public class JwtConverterProperties {

    private String resourceId;
    private String principalAttribute;
}
```

## Rest Controller Package

### Rest Controller Class (ControllerHello.java) 
```
package com.KeycloakApp.KeycloakApp.controller;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class ControllerHello{

    @GetMapping("/hello")
    public ResponseEntity<String> sayHello() {
        return ResponseEntity.ok("Hello");
    }

    @GetMapping("/admin")
    public ResponseEntity<String> sayHelloToAdmin() {
        return ResponseEntity.ok("Hello Admin");
    }

    @GetMapping("/user")
    public ResponseEntity<String> sayHelloToUser() {
        return ResponseEntity.ok("Hello User");
    }

    @GetMapping("/test")
    public String testOutput() {
        System.out.println("Das ist ein TEst");
        return "test";
    }
}
```

