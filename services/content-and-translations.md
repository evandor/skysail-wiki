# Content and Translations

skysail provides a way to **customise the created html pages**, so that you are able to add specific information for the user about the current page's content and purpose. Although the approach of creating skysail pages is very generic and the layout is kind of fixed, using this kind of customisation let's you create very specific content.

The same approach can be used both for providing **custom content **and **internationalisation** \(i18n\).

A **key concept** for this is the utilisation of \(possible multiple\) **TranslationStores** \(to retrieve translations from\) and \(zero or more\) **TranslationRenderService**s \(to format the translations\).

Furthermore, skysail tries to make it easy for the creator of an application to create/alter these translations, so there is a specific _GUI Mode_ to

## Relevant Bundles

* **skysail.api** - interface definitions and Noop Implementations.
* **skysail.server.text.store.bundleresource** - provides a TranslationStore based on property files inside bundles.
* **skysail.server.text.store.inmemory** - provides a TranslationStore based on an in-memory map.
* **skysail.server.text.markdown** - provides a translationRenderServices based on markdown.
* **skysail.server** - utilises the above by providing a "translate" method.

# Core Interfaces, Methods and Implementations

##### Translation \(io.skysail.api.text\) &lt;&lt;Class&gt;&gt;

Defines a _Translation_ object \(which is the result of looking up a key and finding a translation for it\). There might be various Translations for a given key, e.g. differing by _Locale_ or _Store _\(see next section\) they were retrieved from.

##### TranslationStore \(io.skysail.api.text\) &lt;&lt;Interface&gt;&gt;

A TranslationStore implementation provides the "repository" where translations for given keys can be retrieved from \(or persisted to\).

##### ResourceBundleStore \(io.skysail.server.text.store.bundleresource.impl\) &lt;&lt;Class&gt;&gt;

A specific _TranslationStore_, based on property files inside bundles.

##### InMemoryTranslationStore \(skysail.server.text.store.inmemory\) &lt;&lt;Class&gt;&gt;

A specific _TranslationStore_, based on an in-memory map.

##### TranslationRenderService \(io.skysail.api.text\) &lt;&lt;Interface&gt;&gt;

A TranslationRenderService implementation asks a _TranslationStore_ for the translation object for a given key and passes this to its render function to create the translated value.

##### MarkdownTranslationRenderService \(io.skysail.server.text.markdown\) &lt;&lt;Class&gt;&gt;

A specific TranslationRenderService, using markdown syntax.

##### Translation SkysailApplication\#translate\(key, defaultMessage, skysailServerResource\) &lt;&lt;Method&gt;&gt;

A factory method to get a _Translation_ for a given key providing a defaultMessage if not found.

##### Map&lt;String, Translation&gt; SkysailServerResource.getMessages\(Map&lt;String, FormField&gt;\) &lt;&lt;Method&gt;&gt;

Rendering a SkysailResource triggers the translation of all FormField - annotated fields of the associated Entity \(-ies\).

# Usage

There's two things you might want to do with translations: _retrieve_ them, given a key \(and context dependent information like Headers and Locale\). Or set/update them, if you have the permissions and access to the relevant files.

### Translation retrieval

The core logic is contained in the method

io.skysail.core.app.SkysailApplication.translate\(key, defaultMessage, SkysailServerResource\).

What happens here is described in the following steps:

1. If there is no _ServiceListProvider_ available, return a translation based on the defaultMessage.
2. Otherwise, get the best translation \(see below\) from the available TranslationStores. If there is no such thing, return a translation based on the defaultMessage like before.
3. Given a translation, check the rendererServices to render the translation and return it.
4. If the translation was not retrieved from the InMemoryStore, persist it there for faster subsequent retrieval.

##### Best translation

So, what's the best translation? 



