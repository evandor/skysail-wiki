# User Management with skysail.um.repository.filebased

This bundle implements the interface _UserManagementRepository _roughly like this:

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

A matching config file has to be called "users.cfg" and could look like this:

```
users = admin,mira,user

admin.id=#11d2741c-baeb-45bf-8bdd-8a58e983a777
admin.roles = admin,developer,translator
admin.password = $2a$12$52R8v2QH3vQRz8NcdtOm5.HhE5tFPZ0T/.MpfUa9rBzOugK.btAHS
admin.email = evandor@gmail.com
admin.name = "Carsten"
admin.surname = "Gräf"

mira.id=#2
mira.roles = admin,developer
mira.password=$2a$12$52R8v2QH3vQRz8NcdtOm5.HhE5tFPZ0T/.MpfUa9rBzOugK.btAHS

user.id = #3
user.password = $2a$12$52R8v2QH3vQRz8NcdtOm5.HhE5tFPZ0T/.MpfUa9rBzOugK.btAHS
 
```



