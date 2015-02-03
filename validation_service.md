## Validation Service

The validation service returns a pre-configured javax.validation.Validator instance.


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

