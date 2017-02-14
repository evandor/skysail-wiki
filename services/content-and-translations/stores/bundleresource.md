# BundleResource Translation Store

This TranslationStore is implemented in the **skysail.server.text.store.bundleresource** bundle and provides translations \(or simply, content\) from a bundle's i18n property files. Given that you have access to these files on your local machine \(e.g. when developing a new bundle\), such a store can also update translations inside a bundle.

### Translation Retrieval Logic

The default logic follows the following steps:

1. get the _list of accepted languages_ from the request
2. return the first translation if one was found
3. Otherwise return the translation for Locale "en".

Please note that the actual return type of the retrieval methods is Optional&lt;Translation&gt;.

### Translation Persistence Logic

Provided you have access to the bundle's ResourceBundles, you can update or create Translations. Please note that the new translation might not be immediately available. 



