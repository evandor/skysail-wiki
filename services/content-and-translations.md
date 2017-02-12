# Content and Translations

skysail provides a way to **customise the created html pages**, so that you are able to add specific information for the user about the current page's content and purpose. Although the approach of creating skysail pages is very generic and the layout is kind of fixed, using this kind of customisation let's you create very specific content. 

The same approach can be used both for providing custom content and internationalisation \(i18n\).

## Relevant Bundles

* **skysail.api** - interface definitions and Noop Implementations.
* 
# Core Interfaces and Implementations

##### Translation \(io.skysail.api.text\)

Defines a Translation object \(which is the result of looking up a key and finding a translation for it\). There might be various Translations for a given key, e.g. differing by _Locale_ or _Store _\(see next section\) they were retrieved from.

##### TranslationStore \(io.skysail.api.text\) &lt;&lt;Interface&gt;&gt;

A TranslationStore implementation provides the "repository" where translations for given keys can be retrieved from \(or persisted to\).

##### ResourceBundleStore \(io.skysail.server.text.store.bundleresource.impl\)

A specific _TranslationStore_, based on property files inside bundles.

##### TranslationRenderService \(io.skysail.api.text\) &lt;&lt;Interface&gt;&gt;

A TranslationRenderService implementation asks a _TranslationStore_ for the translation object for a given key and passes this to its render function to create the translated value.

##### MarkdownTranslationRenderService \(io.skysail.server.text.markdown\)

A specific TranslationRenderService, using markdown syntax.

# Usage

If you extend a [SkysailApplication](https://github.com/evandor/skysail/blob/master/skysail.server/src/io/skysail/core/app/SkysailApplication.java), you can use the method getMetricsCollector\(\) and use it like this to create a timer metric:

```
TimerMetric timerMetric = getMetricsCollector().timerFor(this.getClass(), "getEntities");
List<T> response = listEntities();
timerMetric.stop();
```

Other metric types can be used accordingly.

