
## Using  User context
Create the usercontext object
```java
@Component
public class UserContext {
    public static final String CORRELATION_ID = "tmx-correlation-id";
    public static final String AUTH_TOKEN = "tmz-auth-token";
    public static final String USER_ID="tmx-user_id";
    public static final String ORGANISATION_ID= "tmx-organisation-id";

    private String correlationId = new String();
    private String authToken = new String();
    private String userId = new String();
    private String organisationId  = new String();

    public String getCorrelationId() {
        return correlationId;
    }

    public void setCorrelationId(String correlationId) {
        this.correlationId = correlationId;
    }

    public String getAuthToken() {
        return authToken;
    }

    public void setAuthToken(String authToken) {
        this.authToken = authToken;
    }

    public String getUserId() {
        return userId;
    }

    public void setUserId(String userId) {
        this.userId = userId;
    }

    public String getOrganisationId() {
        return organisationId;
    }

    public void setOrganisationId(String organisationId) {
        this.organisationId = organisationId;
    }
}



```

A thread local holder for that service

```java
public class UserContextHolder {  
    private static final ThreadLocal<UserContext> userContext = new ThreadLocal<UserContext>();  
  
  
 public static final void setContext(UserContext context) {  
        userContext.set(context);  
 }  
    public static final UserContext createEmptyContext(){  
        return new UserContext();  
 }  
  
    public static final UserContext getContext(){  
        UserContext context = userContext.get();  
 if (context == null) {  
            context = createEmptyContext();  
 userContext.set(context);  
 }  
        return userContext.get();  
 }  
  
  
}


```


FInally a filter put in the values.:-

```java

@Component
@Slf4j
public class UserContextFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest httpServletRequest, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        UserContextHolder.getContext().setCorrelationId(httpServletRequest.getHeader(UserContext.CORRELATION_ID));
        UserContextHolder.getContext().setUserId(httpServletRequest.getHeader(UserContext.USER_ID));
        UserContextHolder.getContext().setAuthToken(httpServletRequest.getHeader(UserContext.AUTH_TOKEN));
        UserContextHolder.getContext().setOrganisationId(httpServletRequest.getHeader(UserContext.ORGANISATION_ID));

        filterChain.doFilter(httpServletRequest,response);
    }
}




```


```java

log.debug("LicenseServiceController Correlation id: {}", UserContextHolder.getContext().getCorrelationId());


```
