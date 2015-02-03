# Documentation Service

A documentation service implementation analyzes a skysail application (its resources, entities and links) and provides a couple of resources documenting those resources. 

## Interface

io.skysail.api.documentation.DocumentationProvider:

    @ProviderType
    public interface DocumentationProvider {
        Map<String, Class<? extends ServerResource>> getResourceMap();
    }
, available in the skysail.api.documentation bundle.


## Default Implementation

io.skysail.server.documentation.SkysailDocumentationProvider


