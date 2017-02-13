# Configuration

In a skysail application, you'll typically find a folder called "_config_", potentially with subfolders for different stages, which contains the applications configuration data inside a couple of files with a "cfg" Suffix.

The path to the configuration files is defined in the bndrun file of your application or product:

```
skysail.config.path = config/local,config/common
logback.configurationFile.path = config/local
```

Here, the logback configuration is looked up in the folder config/local, and other configuration files are looked for in both the folders config/local and config/common.

