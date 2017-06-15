# HelloWorldApplication

So, you already ran the HelloWorldApplication like described [here](/next-steps.md)? And you wonder why this was more than 40MB big? In a programming language, a "HelloWorld" Application is usually very tiny. But skysail is not a programming language, it is a BaaS, a Backend-as-a-Service, and a minimal skysail application will not just print "hello world" - it is a ready-to-run server application, including an http server, an \(in-memory\) database, validation, configuration, user management, security mechanisms and more.

Even though you got one jar only \(plus some self-generating configuration and logs folders\) and this might look like some monolithic approach, skysail is far from being a monolith - it is based on OSGi, and almost every aspect of skysail could be extended or implemented differently.

For example, if you extracted the _skysail.app.helloworld.jar_, you'd find a lot of jars inside, among them one bundle called "_skysail.config.init.jar_". This little fellow is responsible for creating the config folder with some default files if you start skysail and no config folder exists yet. After the first run, you could just delete that file - after all, the config folder is already there. Nothing would break.

Here's a little list of what the HelloWorldApplication is actually doing for you:

### Persistence

You can create multiple "Hello xxx" entries - they will be persisted automatically. If you check the relevant configuration file in config/db-default.cfg, you could change the line 

```
url = memory:helloworld
```

to 

```
url = url = plocal:etc/helloworld
```

Next time you start helloworld, instead of using the default in-memory orientdb database, you will use the file-based version of orientdb, and you hello-world-greetings will actually survive the next restart.

### Configuration

As described under "Persistence", skysail provides a configuration mechanism. 

## Validation

## Security

## User Management 



