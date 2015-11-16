Starling plugin for Apache Maven
---------------------------------

This project provides a [Maven](https://maven.apache.org/) plugin
for [Starling](http://www.mcleodmoores.com/starling).


#### generate-scripts

Phase: prepare-package

Properties:
- skip
 - Set to true to skip all processing, default false
 - Property = "starling.generate.scripts.skip"
- outputDir
 - Where the scripts should be generated, default ${project.build.directory}/scripts
- type
 - The type to generate.
   This is a shortcut, allowing all the files stored in the scripts project
   to be accessed without needing to specify lots of config everywhere.
   The only recognized value at present is 'tool'.
   If this is set, then the unixTemplate and windowsTemplate fields will be
   set, and a standard set of additional scripts added.
   Use the 'unix' and 'windows' boolean flags to control which is output.
 - Property = "starling.generate.scripts.type"
- unix
 - Set to false to turn off generation of Unix scripts, default true.
 - Property = "starling.generate.scripts.unix"
- unixTemplate
 - The basic template file name on Unix.
   This is used as the default template file name.
- windows
 - Set to false to turn off generation of Windows scripts, default true.
 - Property = "starling.generate.scripts.windows"
- windowsTemplate
 - The basic template file name on Windows.
   This is used as the default template file name.
- additionalScripts
 - List of additional scripts to copy unchanged.
- zip
 - Set to false to turn off creation of an attached zip file, default false.
 - Property = "starling.generate.scripts.zip"


#### server-init

These initialize a Starling component server.
They are intended to be run directly from the command line.

The recommended usage is to setup an starling.maven.plugin.properties file, see below.

Properties:
- config
 - The classpath location of an starling-maven.plugin.properties file.
   Any value set in the properties file override command line arguments.
 - Command line property = "config"
- className
 - The initialization class name to run.
 - Command line property = "className"
- configFile
 - The component server properties or INI file.
   The file or classpath prefix is optional, as it will try both.
 - Command line property = "configFile"
- serverLogging
 - The level of logging for the server in general - ERROR, WARN, INFO or DEBUG.
   Default WARN.
 - Command line property = "serverLogging"

Example:

```
 mvn starling:server-init -DconfigFile=toolcontext/toolcontext-examplessimulated.properties

 mvn starling:server-init -Dconfig=fullstack
 // where there is a classpath file fullstack/starling-maven.plugin.properties:
 server.init.class = com.starling.component.OpenGammaComponentServer
 server.init.configFile = classpath:/toolcontext/toolcontext-examplessimulated.properties
```


#### server-run / server-start

These start and stop a Starling component server.
They are intended to be run directly from the command line.

The `server-run` goal will start the server inline so it can be killed by Ctrl+C.

The `server-start` goal will start the server in the background where it must be killed by `server-stop`.

The recommended usage is to setup an starling-maven.plugin.properties file, see below.

Properties:
- config
 - The classpath location of an starling-maven.plugin.properties file.
   Any value set in the properties file override command line arguments.
 - Command line property = "config"
- className
 - The server class name to run.
   The default value of 'com.openemma.component.OpenGammaComponentServer' is generally sufficient.
 - Command line property = "className"
- configFile
 - The component server properties or INI file.
   The file or classpath prefix is optional, as it will try both.
 - Command line property = "configFile"
- startupLogging
 - The level of logging during startup - ERROR, WARN, INFO or DEBUG.
   Default WARN.
 - Command line property = "startupLogging"
- serverLogging
 - The level of logging for the server in general - ERROR, WARN, INFO or DEBUG.
   Default WARN.
 - Command line property = "serverLogging"
- vmMemoryArgs
 - The memory arguments for the server.
   Default values are chosen if not set.
 - Command line property = "vmMemoryArgs"
- vmArgs
 - Any additional VM arguments for the server.
 - Command line property = "vmArgs"

Examples:

```
 mvn starling:server-run -DconfigFile=fullstack/fullstack-examplessimulated-dev.properties

 mvn starling:server-run -Dconfig=fullstack
 // where there is a classpath file fullstack/starling-maven.plugin.properties:
 server.main.class = com.opengamma.component.OpenGammaComponentServer
 server.main.configFile = classpath:/fullstack/fullstack-examplessimulated-dev.properties
```


#### server-stop

This stops a server that was started using `server-start`.

The `server-stop` goal takes no properties.

Example:

```
 mvn starling:server-stop
```


#### Properties file

The command line can be shortened using a properties file name `starling-maven-plugin.properties`.
The only command line argument is to the classpath directory whether the file is located.

The following property keys are recognised:

    server.init.class
    server.init.configFile
    server.init.serverLogging

    server.main.class
    server.main.configFile
    server.main.startupLogging
    server.main.serverLogging
    server.main.vmMemoryArgs
    server.main.vmArgs

The "server.init" keys work with the "server-init" goal.
The "server.main" keys work with the "server-run" and "server-start" goals.
Any value set in the properties file overrides the matching value on the command line.



#### Trademarks

Maven, Apache and Apache Maven are trademarks of The Apache Software Foundation.
