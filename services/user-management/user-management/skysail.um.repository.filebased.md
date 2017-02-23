# User Management with skysail.um.repository.filebased

This bundle implements the interface \_UserManagementRepository \_roughly like this:

```java
@Activate
public synchronized void activate(Map<String, String> config) {
    // create a set of users (and their roles) from the provided configuration
}

@Override
public Optional<User> getUser(String username) {
    return Optional.ofNullable(users.get(username));
}

@Override
public Map<String, User> getUsers() {
    return Collections.unmodifiableMap(users);
}

@Override
public Set<Role> getRoles() {
    return Collections.unmodifiableSet(roles);
}

@Override
public Map<User, Set<Role>> getUsersRoles() {
    return Collections.unmodifiableMap(usersRoles);
}
```

A matching config file has to be called "users.cfg", for an example, check [this ](/configuration/users.md)page.





