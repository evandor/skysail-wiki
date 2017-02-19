# Filtering

Requests are handled using some _filter_ logic, that is, applying a chain of predefined filters to the request. A concrete filter \(re-\)implements the following methods from the abstract class 

  AbstractResourceFilter&lt;R extends SkysailServerResource&lt;?&gt;, T extends Entity&gt;

##### beforeHandle

This method is called before the actual processing logic. If the filter decides to return FilterResult.STOP, the filter chain is stopped and the execution is proceeded in the callers afterHandle method. If the filter returns FilterResult.SKIP, the current filter is skipped and the execution in proceeded in the next filter of the chain.

```java
protected FilterResult beforeHandle(R resource, Wrapper<T> responseWrapper) {
    return FilterResult.CONTINUE;
}
```

##### doHandle

The actual business logic implemented by this filter. Check the concrete implementations on the following pages for examples.

```java
protected FilterResult doHandle(R resource, Wrapper<T> responseWrapper) {
   ...
}
```

##### afterHandle

Sometimes is makes sense to post-process the request \(or resource\)

```java
protected void afterHandle(R resource, Wrapper<T> responseWrapper) {
    // default implementation doesn't do anything
}
```



