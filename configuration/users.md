# Users

### Purpose

If you use the bundle **skysail.um.repository.filebased**, ** **you have to provide a configuration file containing users, encrypted password and user-role associations in a specific format.

### Config File Name

us_ers.cfg_ \(located in one of the [configuration folders](/configuration.md)\).

### Example

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

In the first line, you list all user names, separated with a comma. Then, for each username you define additional attributes \(id, password, roles and so on\) like in the example above.

