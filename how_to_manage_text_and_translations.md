# How to... manage text and translations

Make sure you have a top-level-folder *resources* in your project and create a subfolder *translations* with a file *messages.properties*.

In the bnd file, you have to add the top-level resource folder to the list of included resources: 

```
Include-Resource: resources
```
If you want to override the default templates, you'll have to define something like this:

```
Include-Resource: resources, templates=src;recursive:=true;filter:=*.st|*.stg
```
