To repro:

build with buck:

i.e.

`./buckw build //app:bin_debug`

and observe:

```
Buck encountered an internal error
java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
	at com.facebook.buck.jvm.kotlin.JarBackedReflectedKotlinc.buildWithClasspath(JarBackedReflectedKotlinc.java:208)
	at com.facebook.buck.jvm.kotlin.KotlincStep.execute(KotlincStep.java:96)
	at com.facebook.buck.step.DefaultStepRunner.runStepForBuildTarget(DefaultStepRunner.java:45)
	... 16 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at com.facebook.buck.jvm.kotlin.JarBackedReflectedKotlinc.buildWithClasspath(JarBackedReflectedKotlinc.java:199)
	... 18 more
Caused by: java.lang.NoClassDefFoundError: gnu/trove/THashMap
	at org.jetbrains.kotlin.com.intellij.openapi.vfs.CharsetToolkit.<clinit>(CharsetToolkit.java:104)
	at org.jetbrains.kotlin.com.intellij.util.LineSeparator.<init>(LineSeparator.java:31)
	at org.jetbrains.kotlin.com.intellij.util.LineSeparator.<clinit>(LineSeparator.java:22)
	at org.jetbrains.kotlin.cli.common.messages.PlainTextMessageRenderer.<clinit>(PlainTextMessageRenderer.java:51)
	at org.jetbrains.kotlin.cli.common.messages.MessageRenderer.<clinit>(MessageRenderer.java:29)
	at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:39)
	... 23 more
Caused by: java.lang.ClassNotFoundException: gnu.trove.THashMap
	at java.net.URLClassLoader.findClass(URLClassLoader.java:382)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 29 more

    When running <kotlinc>.
    When building rule //app:src_debug.
```

A subsequent build has a different stacktrace:
```
Buck encountered an internal error
java.lang.RuntimeException: java.lang.reflect.InvocationTargetException
	at com.facebook.buck.jvm.kotlin.JarBackedReflectedKotlinc.buildWithClasspath(JarBackedReflectedKotlinc.java:208)
	at com.facebook.buck.jvm.kotlin.KotlincStep.execute(KotlincStep.java:96)
	at com.facebook.buck.step.DefaultStepRunner.runStepForBuildTarget(DefaultStepRunner.java:45)
	... 16 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at com.facebook.buck.jvm.kotlin.JarBackedReflectedKotlinc.buildWithClasspath(JarBackedReflectedKotlinc.java:199)
	... 18 more
Caused by: java.lang.NoClassDefFoundError: Could not initialize class org.jetbrains.kotlin.cli.common.messages.MessageRenderer
	at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:39)
	... 23 more

    When running <kotlinc>.
    When building rule //app:src_debug.
```


This only happens with Kotlin 1.3.20
