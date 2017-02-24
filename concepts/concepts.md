# Concepts

In some way, skysail is just a set of concepts.

When you create something like a library or any kind of software others might want to use, you have to make a lot of decisions. Some of those might be easy - for example, picking a specific programming language. Others, like deciding if you really want to depend on other libraries and/or frameworks \(and which ones\) are harder. And, of course, you have some kind of problem in mind you want to solve.

So, in the end, you decide about a lot of things and create something which \(hopefully\) is useful - but only to people having this kind of problem, using that specific programming language and have a similar set of dependencies as you.

This chapter is about the decisions I've done.

All the concepts like "Applications", "Business Logic" and "Request Processing" - they might be valuable to only a small set of people. Still, I think these concepts are useful to solve problems I am confronted with, and I am happy to discuss \(and adjust\) them. Maybe they are useful to somebody else as well - hopefully, as this is the reason I started this in the first place.

The **two big **decisions right at the beginning were:

* the programming language \(**Java**\)
* and the "framework" \(**OSGi** \[with bndtools\]\)

For those still reading on ;\):

Picking this combination has a few implications: Actually, the programming language is not really restricted to Java: You can use any language running on the Java Virtual Machine \(like Scala, Groovy, Clojure, ...\). And, there is a clean modularization between the various parts. New Applications can be deployed into a running installation without restarting. If you are afraid to do this in production, you'll still love it in development. Dependencies are well-expressed and clean.

Round about a hundred bundles for a typical skysail installation seem a lot. But it's not: you'll get the server \(jetty\), a database \(orientdb\), serialization features \(jackson\) and validation stuff \(hibernate\). And more. Using OSGi let's you pick between various implements of specific features easily \(for example, where do you store your users, if at all\) - and, if you don't find what you are looking for - implement it yourself. Replace the implementation you are not happy with, and it will work.

And: your _deployable_, it's just a single jar file. You start it like "java -jar myskysail.installation.jar". That's it. Database and server included. 

