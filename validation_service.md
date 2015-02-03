## Validation Service

The validation service returns a (pre-configured) javax.validation.Validator instance which can be used to validate JavaBeans as specified in JSR 303.

In skysail, this service is used in de.twenty11.skysail.server.core.restlet.filter.CheckBusinessViolationsFilter in order to validate all entities retrieved by the server. 


### Interface

io.skysail.api.validation.ValidatorService in bundle skysail.api.validation.

````
import javax.validation.Validator;

import aQute.bnd.annotation.ProviderType;

@ProviderType
public interface ValidatorService {

    Validator getValidator();

}
````
Defined in skysail.api.validation bundle.


### Implementations

io.skysail.api.validation.hibernate.DefaultValidationImpl in skysail.api.validation (same bundle as the interface).

This implementation utilizes the Hibernate validator and configures it so that it can be used in the OSGi framework.



