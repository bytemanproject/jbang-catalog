# Byteman jbang catalog

This catalog enables using byteman via [jbang.dev](https://jbang.dev).

The usecase for jbang with byteman is that you do not need to download/install
byteman manually. Useful if exploring things on a new/remote system or in a container.

## Run applications with jbang and byteman 

To run a jar, maven artifact or jbang script with byteman as agent:

```
jbang --javaagent byteman@bytemanproject your.jar
jbang --javaagent byteman@bytemanproject org.group:artifact:version
jbang --javaagent byteman@bytemanproject alias@catalog
```

To load scripts use the normal byteman flags:

```
jbang --javaagent byteman@bytemanproject:script=myfile.btm your.jar
```

Using JBang 0.104 or newer you can even load remote files:

```
jbang --javaagent byteman@bytemanproject:script=%{https://url/to/myfile.btm} your.jar
```

If you need to add byteman or other jars to boot classpath you can use this trick:

```
 jbang --javaagent=byteman@bytemanproject=boot:`jbang info classpath byteman@bytemanproject` your.jar
```

Combining it all you can do this:

```
 jbang --javaagent=byteman@bytemanproject=boot:`jbang info classpath byteman@bytemanproject`,script:%{https://github.com/bytemanproject/byteman/raw/main/sample/scripts/FileMonitor.btm} jarviz@kordamp
```

This runs `jarviz@kordamp` loads the `byteman@bytemanproject` as a javaagent, adds the necessary classpath to boot path and remotely fetches the FileMonitor.btm available in byteman main repo.

All without requiring to install or setup byteman nor java.

## Install Byteman remotely

To install Byteman on a remote system you can use the `bminstall` command:

```
jbang bminstall@bytemanproject -b <pid>
```

## Submit Byteman scripts remotely

To submit byteman scripts to a remote system you can use the `bmsubmit` command:

```
jbang bmsubmit@bytemanproject myfile.btm
```

## Check byteman scripts

To check your byteman scripts you can use the `bmcheck` command:

``` 
jbang bmcheck@bytemanproject myfile.btm
```

