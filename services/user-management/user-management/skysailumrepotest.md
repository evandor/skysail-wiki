# User Management with skysail.um.repo.test

This bundle implements the interface _UserManagementRepository_ roughly like this:

```java
// start with an empty Map (username -> User)
val users = scala.collection.mutable.Map[String, User]()

public Optional<User> getUser(String username) {
  // if the username exits in the users map, return it.
  // Otherwise, add the user with its username as password and roles ("user", username)
}
```

So, using skysail.um.repo.test will give you an implementation which, for example, accepts the username "admin", provided is the password provided is "admin", and the user will have the roles "user" and "admin".

