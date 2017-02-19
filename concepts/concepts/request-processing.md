# Request Processing

**Request processing** is crucial for a BaaS like skysail. There's a predefined, generic way each GET, POST, PUT and DELETE request is handled. The **restlet framework** used by skysail handles a lot of request-processing related logic, especially how the actual resource serving the request is determined. There's an association between one \(or more\) **endpoint** urls and the concrete resource to handle the request.

Depending on the [endpoint semantic](/conventions.md), a specific kind of resource class will provide the request processing logic:

* **ListServerResource** - returns a list representation of entities and provides deletion logic.
* **EntityServerResource** - returns a representation of a concrete entity defined by its id.
* **PostEntityResource** - creates a new entity \(or provides you with an entity template for creation\).
* **PutEntityResource** - updated an existing entity \(or provides you with an template for updating\).

The media types recognised by the various resources are explained in detail on the next pages.



