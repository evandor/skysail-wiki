# Authentication with skysail.um.httpbasic

This bundle implements the AuthenticationSercive Interface \(defined in skysail.api\) roughly like this:

```java
(...) 

public HttpBasicAuthenticationService(HttpBasicUserManagementProvider userManagementProvider) {
    ...
}

@Override
public Authenticator getApplicationAuthenticator(Context context) {
    // return an Authenticator which always yields "true" 
}

@Override
public Authenticator getResourceAuthenticator(Context context) {
    // return a restlet ChallengeAuthenticator for the challenge schema "HTTP_BASIC".
}

@Override
public Principal getPrincipal(Request request) {
    // get the user from the "Authorization" header or return an "anonymous user".
}

@Override
public boolean isAuthenticated(Request request) {
    return !getPrincipal(request).getName().equals(ANONYMOUS);
}

@Override
public String getLoginPath() {
    // more or less this:
    return "/" + HttpBasicUmApplication.class.getSimpleName() + "/v1" + SkysailRootApplication.LOGIN_PATH;
}

@Override
public String getLogoutPath() {
    // HTTP Basic does not provide anything like "log out".
    return null;
}
```

As you can see, the constructor needs an UserManagementProvider, which is responsible for providing the users who can use the system.

