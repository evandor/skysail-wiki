# Users, Authentication & Authorization

User Managment is a big topic and there are three sub-chapters dealing with Authentication, Authorization and the actual management of users and their roles.

## Relevant Bundles

* **skysail.api** - interface definitions.
* **skysail.um.httpbasic** - .
* .

# Overview

The central user management interface \(including authentication and authorization\) is the "UserManagementProvider", which provides access to an _AuthenticationService_, an _AuthorizationService_ and a_ UserManagementRepository_. Typically, a bundle will implement the two services itself and rely on an external UserManagementRepository, provided by another bundle.

![](/assets/um.png)

# Usage

Todo

```
todo
```

Todo.

