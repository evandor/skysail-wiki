# Metrics

Metrics is a service helping developers to **measure various metrics inside their code**, for example, methods' execution time.

## Relevant Bundles

* **skysail.api** - interface definitions and Noop Implementations.
* **skysail.core** \(former skysail.server\) - utilises _metrics_ if \(at least\) one implementation is available in the runtime.
* **skysail.server.ext.metrics** - bundle providing an [MetricsImplementation](https://github.com/evandor/skysail/blob/master/skysail.api/src/io/skysail/api/metrics/MetricsImplementation.java) based on [Dropwizard](http://metrics.dropwizard.io/). 
* **skysail.server.app.metrics** - access to collected metrics and visualisation.

# Supported Metrics

* **Counters** - increment and decrement an integer \(e.g. count of current active sessions\)
* **Histogram** - measures the distribution of values in a stream of data: e.g., the number of results returned by a search
* **Meter** - measures the _rate _at which a set of events occur: e.g., requests per minute
* **Timer** - measure the duration \(and distribution\) of a type of event: e.g., page rendering.

# Usage

If you extend a [SkysailApplication](https://github.com/evandor/skysail/blob/master/skysail.server/src/io/skysail/core/app/SkysailApplication.java), you can use the method getMetricsCollector\(\) and use it like this to create a timer metric:

```
TimerMetric timerMetric = getMetricsCollector().timerFor(this.getClass(), "getEntities");
List<T> response = listEntities();
timerMetric.stop();
```

Other metric types can be used accordingly.







