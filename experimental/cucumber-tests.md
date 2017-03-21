# Cucumber Tests

## Setup

### bnd.bnd File

```
-buildpath: \
    ...
    ${cucumber},\
```

### cucumber.properties

located in /test:

```
cucumber.api.java.ObjectFactory = io.skysail.server.testsupport.CustomPicoFactory
```

### RunCucumberTests.java

located in /test/io.skysail....test/

```
import org.junit.runner.RunWith;
import cucumber.api.CucumberOptions;
import cucumber.api.junit.Cucumber;

@RunWith(Cucumber.class)
@CucumberOptions(
        tags = {"@singleEntityRefApplication"},
        glue   = { "io.skysail.server.app.ref.singleentity" },
        plugin = { "pretty", "json:generated/cucumber.json", "html:generated/cucumber" }
)
public class RunCucumberTests { // NOSONAR

}

```



