# Links

Handling links is a central concept in skysail, and it is based on the ideas of HATEOAS. 

Each response to a request contains Linkheaders, pointing to the next possible resources which can be reached from the current one. A linkheader looks something like this \(apart from formatting\):

```
Link:</bookmarks/v1/bookmarks/>; rel="create-form"; title="post bookmark"; verbs="GET,POST",
     </bookmarks/v1/bookmarks/{id}/>; rel="edit-form"; title="update bookmark"; verbs="GET,PUT",
     </bookmarks/v1/bookmarks/{id}>; rel="item"; title="show"; verbs="GET"
```

Each link information is separated by a comma and contains the actual link, a relation descriptor, a title and a list of http verbs which can be used with the link.

