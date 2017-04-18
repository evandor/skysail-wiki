# Authentication

Typically, you want your users to **authenticate **when using a web _application _\(as opposed to most _web sites_ which are meant for reading\). Authentication can be done is various ways, and skysail provides a couple of bundles \(see Chapter "User Management"\) you can choose from. If it comes to authentication, those bundles need to provide a class implementing the following interface from **skysail.api**:

```java
public interface AuthenticationService {

    /**
     * @return a restlet authenticator the application is authenticated against.
     */
    Authenticator getApplicationAuthenticator(Context context, AuthenticationMode authMode);

    /**
     * @return a restlet authenticator the applications' resources are
     *         authenticated against.
     */
    Authenticator getResourceAuthenticator(Context context, AuthenticationMode authMode);

    /**
     * @return whether or not the current request is authenticated.
     */
    boolean isAuthenticated(Request request);

    /**
     * @return the associated principal, i.e. the currently authenticated user.
     */
    Principal getPrincipal(Request request);

    /**
     * skysail can be set up to run with different authentication services, which
     * typically provide a login path to which the generic "/_login" path will
     * be redirected.
     */
    String getLoginPath();

    /**
     * skysail can be set up to run with different authentication services, which
     * typically provide a logout path to which the generic "/_logout" path will
     * be redirected.
     */
    String getLogoutPath();
}
```

The simplest of these bundles is **skysail.server.um.httpbasic, **which provides an authentication scheme based on "[HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)". Another bundle is **skysail.server.um.shiro**, utilizating the apache project [shiro](https://shiro.apache.org/). Authentication is not trivial and skysail doesn't try to reinvent the wheel - if needed, it simply delegates to other libraries to do the job \(they were made for\). Futher bundles are planed for, and, of course, you could create your own bundle implementing the interface above to create your own authentication service.

