# Spring Security with Okta
[Spring Security With Okta](https://www.baeldung.com/spring-security-okta)
[Demo Repository](https://github.com/eugenp/tutorials.git)
[Demo Source](https://github.com/eugenp/tutorials/spring-security-modules/spring-security-okta)

## JPA Project Setup
```
src/
├── main/
│   └── java/
|       ├── Application.java
|       └── rest/
|           ├── AdminController.java
|           ├── HomeController.java
└── resources/
    └── application.properties
```

## Application Properties
```
server.port=8081

#
# Okta properties
#
okta.oauth2.issuer=https://dev-15903420.okta.com/oauth2/default
#okta.oauth2.issuer=https://dev-15903420.okta.com/oauth2/ausg6mxp6o55un1pz5d7
okta.oauth2.client-id=<clientid>
okta.oauth2.client-secret=<client-secret>
#okta.oauth2.redirect-uri=http://localhost:8080/authorization-code/callback
okta.oauth2.redirect-uri=/authorization-code/callback

okta.client.orgUrl=https://dev-xyz.okta.com
okta.client.token=<client-token>
```

## Application (Application.java)
```
package com.coresoftware.oktademo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class OktademoApplication {

	public static void main(String[] args) {
		SpringApplication.run(OktademoApplication.class, args);
	}
}
```

## Rest Controller
### Admin Controller Class (AdminController.java)
```
package com.coresoftware.oktademo;

import com.okta.sdk.client.Client;
import com.okta.sdk.resource.user.UserList;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class AdminController {
    @Autowired
    public Client client;

    @GetMapping("/users")
    public UserList getUsers() {
        // Example: http://localhost:8080/users
        return client.listUsers();
    }

    @GetMapping("/user")
    public UserList searchUserByEmail(@RequestParam String query) {
        // Example: http://localhost:8080/user?query=sacha.dubois@icloud.com
        return client.listUsers(query, null, null, null, null);
    }
}
```

### Home Controller Class (HomeController.java)
```
package com.coresoftware.oktademo;

import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.security.oauth2.core.oidc.user.OidcUser;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HomeController {
    @GetMapping("/")
    public String home(@AuthenticationPrincipal OidcUser user) {
        return "Welcome, "+ user.getFullName() + "!";
    }
}
```

