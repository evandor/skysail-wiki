# Applications

When it comes to skysail, as a developer, you can extend \(and/or\) fix its core functionality, or you can create **Applications**.

An _application_ is a **cohesive unit** \(in DDD: a bounded context\) of functionality, expressed as a **domain model**, the** associated business logic **and made available to the outside world as a set of **RESTful endpoints**. And, it is an **OSGi bundle**.

This bundle can be deployed into the skysail server, and, given its dependencies are matched, its endpoints will be available for provisioning and consumption.

# Overview

to be done

# Configuration

There are \(at least\) two ways to configure an application: There's the general one, which can be applied to all applications and contains definitions, for example, for CORS configuration. And then, often, you might need application-specific configurations, for example file paths or database access tokens.

### General Configuration

This kind of config is described [here](/configuration/applidation-and-cors.md).

### Application-Specific Configuration 

Let's use an example here: let's assume we have an application which utilizes the spotify API. So we need to configure a clientId, a clientSecret and the redirectUrl. This information should not be hardcoded, we don't even want to put it in version control. What we do is to define a configuration description and a configuration provider:

The configuration description:

```java
import org.osgi.service.metatype.annotations.ObjectClassDefinition;

@ObjectClassDefinition(name = "Spotify Config")
public @interface SpotifyConfigDescriptor {
    String clientId() default "";
    String clientSecret() default "";
    String redirectUri() default "";
}

```

This file defines what to expect inside a configuration file \(and could provide defaults as well\). Then we create an OSGi component which will make the configuration data available to our application:

```
import org.osgi.service.component.ComponentContext;
import org.osgi.service.component.annotations.Activate;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.ConfigurationPolicy;
import org.osgi.service.component.annotations.Deactivate;
import org.osgi.service.metatype.annotations.Designate;

import lombok.Getter;

@Component(
    immediate = true, 
    configurationPolicy = ConfigurationPolicy.OPTIONAL, 
    configurationPid = "spotify", 
    service = SpotifyConfiguration.class)
@Designate(ocd = SpotifyConfigDescriptor.class)
public class SpotifyConfiguration {

    @Getter
    private SpotifyConfigDescriptor config;

    @Activate
    public void activate(SpotifyConfigDescriptor config) {
        this.config = config;
    }

    @Deactivate
    protected void deactivate(ComponentContext ctxt) {
        config = null;
    }
}
```

Given a configuration file with the name "spotify.cfg" \(see configurationPid\) inside on of the configuration folders with contents like this

```
clientId=abc...
clientSecret=123...
redirectUri=http://localhost:2021/spotify/v1/callback

```

the SpotifyConfiguration will be instantiated by the framework and will receive the data defined in the config file. You now can access this somewhere else in your application like this:

```
import org.osgi.service.component.annotations.Component;
import io.skysail.app.spotify.config.SpotifyConfiguration;
...

@Component(immediate = true, configurationPolicy = ConfigurationPolicy.OPTIONAL)
public class SpotifyApplication extends SkysailApplication implements ApplicationProvider, MenuItemProvider {
    
    @Reference
    @Getter
    private SpotifyConfiguration config;
    ...
}
```



