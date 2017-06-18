# skysail...

##### ...is: a modular, domain-centric and RESTful BaaS \(Backend as a Service\)

###### \(That you can host yourself\)

The overall goal of skysail is to provide you with an environment where you can create **typical backend logic in a generic, quick way** with as **little dependencies** as possible. This makes skysail suited for _prototypes_, first of all, but I hope that this approach - even if generic - is good enough for production ready _applications_ as well.

Typical backend logic covered by skysail:

* **Authentication** / **Authorization**
* **Security** **aspects** \(like injection\)
* **Configuration**
* **Validation**
* **Documentation**
* **Persistence**

We have some more things skysail could help you with:

* **User Management**
* **HTML Rendering** \(Template Engine\)
* and - **calling other APIs**

### Modularity

skysail is a **collection of OSGi bundles**, depending on other bundles, and defining an API for domains like authentication, security, persistence and so on. If some API implementation does not fulfil your needs, it is easy to replace it with your own implementation.

### Domain-Centric

skysail lets you **concentrate on your business \(or domain\) logic**. Http Server, database, configuration setup and the like are already there. Just use them.

### RESTful

skysail concentrates on the backend and tries to stick to RESTful principles.

### BaaS

skysail is a [Backend-as-a-Service](https://en.wikipedia.org/wiki/Mobile_backend_as_a_service).

### Self-Hosting

The difference to other BaaS, you can download and run skysail on your own machines.

