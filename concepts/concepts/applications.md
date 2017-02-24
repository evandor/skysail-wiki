# Applications

When it comes to skysail, as a developer, you can extend \(and/or\) fix its core functionality, or you can create **Applications**.

An _application_ is a **cohesive unit** \(in DDD: a bounded context\) of functionality, expressed as a **domain model**, the** associated business logic **and made available to the outside world as a set of **RESTful endpoints**. And, it is an **OSGi bundle**.

This bundle can be deployed into the skysail server, and, given its dependencies are matched, its endpoints will be available for provisioning and consumption.



