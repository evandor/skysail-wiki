# ExceptionCatchingFilter

### Purpose

This filter usually is the first filter in the chain and is used to wrap the following executions inside a try-catch statement, in order to handle exceptions in a consistent way. 

##### beforeHandle

```java
default
```

##### doHandle

```java
try {
    super.doHandle(resource, responseWrapper);
} catch (ResourceException re) {
    throw re;
} catch (Exception e) {
    ExceptionCatchingFilterHelper.handleError(e, application, responseWrapper, resource.getClass());
}
```

##### afterHandle

Sometimes is makes sense to post-process the request \(or resource\)

```java
protected void afterHandle(R resource, Wrapper<T> responseWrapper) {
    // default implementation doesn't do anything
}
```



