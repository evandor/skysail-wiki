# HelloWorldApplication

So, you already ran the HelloWorldApplication like described [here](/next-steps.md)? And you wonder why this was more than 40MB big? In a programming language, a "HelloWorld" Application is usually very tiny. But skysail is not a programming language, it is a BaaS, a Backend-as-a-Service, and a minimal skysail application will not just print "hello world" - it is a ready-to-run server application, including an http server, an \(in-memory\) database, validation, configuration, user management, security mechanisms and more.

Even though you got one jar only \(plus some self-generating configuration and logs folders\) and this might look like some monolithic approach, skysail is far from being a monolith - it is based on OSGi, and almost every aspect of skysail could be extended or implemented differently.

For example, if you extracted the _skysail.app.helloworld.jar_, you'd find a lot of jars inside, among them one bundle called "_skysail.config.init.jar_". This little fellow is responsible for creating the config folder with some default files if you start skysail and no config folder exists yet. After the first run, you could just delete that file 

