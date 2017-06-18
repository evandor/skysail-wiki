# ListServerResource\[T\]

If you havn't read the intro about skysail resources, you'll find it [here](/resources.md).

### Overview

A _ListServerResource_ is a _SkysailServerResource_ parameterized with a **List** of some Type. It's purpose is to provide endpoints for listing multiple entities of the same kind: Implementing a specific ListServerResource could, for example, give you a list of notes, customers, connections, whatever. 

These lists can be paginated and sorted, and they can be retrieved as html, json, xml and so on.



