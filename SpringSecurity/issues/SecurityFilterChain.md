
# SecurityFilterChain 

## permitAll() not working correctly for non authorisation endpoints
If there are endpoints defined ie '/welcome' where clints do not need to authenticate, the permitAll() rules seams not to work correctly as request are redirectd to get authentificated.

```
package com.luv2code.springboot.cruddemo.security;

import jakarta.servlet.DispatcherType;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;
import org.springframework.http.HttpMethod;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.builders.WebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
import org.springframework.security.web.servlet.util.matcher.MvcRequestMatcher;
import org.springframework.web.servlet.handler.HandlerMappingIntrospector;

import static org.springframework.security.config.http.MatcherType.mvc;

@Configuration
public class DemoSecurityConfig {
    @Bean
    public InMemoryUserDetailsManager userDetailsManager() {
        UserDetails john = User.builder()
                .username("john")
                .password("{noop}test123")
                .roles("EMPLOYEE")
                .build();

        UserDetails mary = User.builder()
                .username("mary")
                .password("{noop}test123")
                .roles("EMPLOYEE", "MANAGER")
                .build();
        UserDetails susan = User.builder()
                .username("susan")
                .password("{noop}test123")
                .roles("EMPLOYEE", "MANAGER", "ADMIN")
                .build();

        return new InMemoryUserDetailsManager(john, mary, susan);
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http, MvcRequestMatcher.Builder mvc) throws Exception {
        http.csrf(csrf -> csrf
                //.csrfTokenRequestHandler(csrfRequestHandler)
                .ignoringRequestMatchers("/api/gugu")
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()));

        http
                .authorizeHttpRequests(configurer ->
                    configurer
                        .requestMatchers(HttpMethod.GET, "/api/hello").permitAll()
                        .requestMatchers(HttpMethod.POST, "/api/hello").permitAll()
                        .requestMatchers(HttpMethod.DELETE, "/api/hello").permitAll()
                        .requestMatchers(HttpMethod.GET, "/api/employees").hasRole("EMPLOYEE")
                        .requestMatchers(HttpMethod.GET, "/api/employees/**").hasRole("EMPLOYEE")
                        .requestMatchers(HttpMethod.POST, "/api/employees").hasRole("MANAGER")
                        // SpringDataRest requires "/api/employees/**" instead of "/api/employees"
                        .requestMatchers(HttpMethod.PUT, "/api/employees/**").hasRole("MANAGER")
                        .requestMatchers(HttpMethod.DELETE, "/api/employees/**").hasRole("ADMIN")
                )

                .authorizeHttpRequests(request ->
                    request
                        .dispatcherTypeMatchers(DispatcherType.FORWARD, DispatcherType.ERROR).permitAll()
                        .requestMatchers(mvc.pattern("/api/gugu"), mvc.pattern("/welcome")).permitAll()
                        .anyRequest().authenticated()
                        //.requestMatchers(HttpMethod.GET, "/api/gugu/**").permitAll()
                       // .requestMatchers(HttpMethod.DELETE, "/api/gugu/**").permitAll()

        );

        /// User HTTP Basic Aithentification
        http.httpBasic(Customizer.withDefaults());

        // disable Cross Site Request Forgery (CSRF)
        // in general not required for stateless REST API's that use POST, PUT, DELETE and/or PATCH
        //http.csrf(csrf -> csrf.disable());

        return http.build();
    }

    @Scope("prototype")
    @Bean
    MvcRequestMatcher.Builder mvc(HandlerMappingIntrospector introspector) {
        return new MvcRequestMatcher.Builder(introspector);
    }
}

```

[Solution Reference](https://github.com/spring-projects/spring-security/issues/14011) 

