# User Management

User Managment is a big topic and there are three sub-chapters dealing with _Authentication_, _Authorization _and the actual _management of users and their roles_.

## Relevant Bundles

* **skysail.api** - interface definitions.
* **skysail.core** \(former skysail.server\) - .
* **skysail.server.um.httpbasic** - .
* .

# Usage

If you extend a [SkysailApplication](https://github.com/evandor/skysail/blob/master/skysail.server/src/io/skysail/core/app/SkysailApplication.java), you can use the method getMetricsCollector\(\) and use it like this to create a timer metric:

```
timerMetric.stop();
```

Other metric types can be used accordingly.

