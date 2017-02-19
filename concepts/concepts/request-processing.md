# Request Processing

**Request processing** is crucial for a BaaS like skysail. There's a predefined, generic way each GET, POST, PUT and DELETE request is handled. The **restlet framework** used by skysail handles a lot of request-processing related logic, especially how the actual resource serving the request is determined. There's an association between one \(or more\) **endpoint** urls and the concrete resource to handle the request.

Depending on the endpoint semantic, a specific kind of resource class will provide the request processing logic:

* ListServerResource - handles list requests
* EntityServerResource
* PostEntityResource
* PutEntityResource



