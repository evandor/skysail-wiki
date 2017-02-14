# InMemory Translation Store

This TranslationStore is implemented in the **skysail.server.text.store.inmemory** bundle and provides translations \(or simply, content\) from a volatile in-memory Map. Updating a translation in this map only makes sense during the execution time, as it will not be permanently persisted. 

The InMemory Translation Store \(if deployed\) has a special purpose inside skysail: Whenever a translation is retrieved from a different store, it will be immediately saved into the In-Memory Store, so the next time the key is requested for a translation, it will be looked up here.

### Service Ranking

The service ranking for this service is **1000**.

This is important for the retrieval of the "best translation", which is based on the service ranking of the store. The InMemory service, for example, ranks higher than the [ResourceBundle](/services/content-and-translations/stores/bundleresource.md) Translation Store.

### Translation Retrieval Logic

The default logic follows the following steps:

1. 
Please note that the actual return type of the retrieval methods is Optional&lt;Translation&gt;.

### Translation Persistence Logic



