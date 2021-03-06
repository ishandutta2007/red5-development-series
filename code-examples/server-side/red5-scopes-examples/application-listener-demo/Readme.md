# Application Listener Example
---

## About
---

This example showcases the `IApplication` interface of Red5 java api. Red5 provides an interface called [IApplication](http://red5.org/javadoc/red5-server-common/org/red5/server/adapter/IApplication.html). An implementation object of this interface can be used as an application listener.

The example registers an `IApplication` implementation called `ApplicationMonitor.java`. The application listener lets you handle core application events related to the application, scopes and connections. You can define multiple application listeners for an application.


## Build & Deploy
---

### Build
---

To build this application : open a shell prompt in the application's project directory (where the pom.xml file resides). run the following maven command in your shell -> 

``` 
mvn clean package 

```

The above command will generate a `war` file in the `target` directory inside the project directory. 


### Deploy
---

To deploy the war to red5 / red5 pro server :

1. Stop server if it is running.

2. Extract the content of the `war file` to directory by war name. 

> The java war file is simply a `archive file` similar to `zip` format. you can extract it using a archive tool such as [7zip](#http://www.7-zip.org/), [Winrar trial](#http://www.rarlab.com/download.htm) etc

3. Copy the folder into `RED5_HOME/webapps/` directory.

4. Start server.


## How To Use Example
---

So use this example application you can use a RTMP or RTSP (Android/IOS) or WebRTC (Red5pro HTML5 SDK) client to connect to and disconnect from the application. You can connect at the application level or to a sub-scope level within the application. 

For each application event, you will observe that the `ApplicationMonitor.java` handles and logs out the various application callbacks such as appStart, appConenct, appDisconenct, roomStart, roomConenct etc.


The `ApplicationMonitor.java` class also demonstrates the use of the utility class `ScopeUtils` to resolve different scope references such as :

1. Finding root scope from any scope

2. Finding application scope from any scope

3. Resolving to a sub-scope reference from application scope when sub-scope path is known.


## Eclipse
---

You can edit the server side code in your eclipse JEE IDE such as Luna, Mars, Neon etc. To import the code into your IDE:

1. Navigate to the repository folder
2. Execute maven command `mvn eclipse:eclipse`. This will generate files necessary for eclipse to read the maven project properly.
3. In eclipse go to `File -> Import -> Existing Maven Projects` and click `Next`.
4. Browse and select `the project root` and Click `Finish` to import the project.



## Additional Notes
---

An application listener is very useful in Red5 plugins to track application callbacks outside the application adapter ([MultiThreadedApplicationAdapter](http://red5.org/javadoc/red5-server/org/red5/server/adapter/MultiThreadedApplicationAdapter.html)). 

You can register an `IApplication` implementation on the application adapter from anywhere using the [addListener](http://red5.org/javadoc/red5-server/org/red5/server/adapter/MultiThreadedApplicationAdapter.html#addListener(org.red5.server.adapter.IApplication)) method as long as you have access to the **application** scope.

__Snippet__

``` 
MultiThreadedApplicationAdapter adapter = (MultiThreadedApplicationAdapter) scope.getHandler();
adapter.addListener(new ApplicationMonitor());
```



