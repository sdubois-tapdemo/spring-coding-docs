# Logging
Spring Profiles provide a way to segregate parts of your application configuration and make it be available only in certain environments. Any @Component, @Configuration or @ConfigurationProperties can be marked with @Profile to limit when it is loaded,.
[Spring Profiles](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.profiles)

# Set Profile with Environment Variable
```
export SPRING_PROFILES_ACTIVE=local
```

# Set Profile with Environment Variable
```
mwn spring-boot:run -Dspring-boot.run.profiles=local
```


