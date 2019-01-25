To repro:

build with gradle:

i.e.

`./gradlew assembleDebug`

and observe:

```
w: Runtime JAR files in the classpath have the version 1.2, which is older than the API version 1.3. Consider using the runtime of version 1.3, or pass '-api-version 1.2' explicitly to restrict the available APIs to the runtime of version 1.2. You can also pass '-language-version 1.2' instead, which will restrict not only the APIs to the specified version, but also the language features
e: warnings found and -Werror specified
w: /Users/michael_dang/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib-common/1.2.60/d95e6419da840e672342e5d4348f0bdd1d58b84d/kotlin-stdlib-common-1.2.60.jar: Runtime JAR file has version 1.2 which is older than required for API version 1.3
w: /Users/michael_dang/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/1.2.60/391695759d8fc80042c2c11bc19fc6f2787be495/kotlin-stdlib-1.2.60.jar: Runtime JAR file has version 1.2 which is older than required for API version 1.3
> Task :app:compileDebugKotlin FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:compileDebugKotlin'.
> Compilation error. See log for more details
```

Although the Kotlin version is set to 1.2.60

This error goes away if you comment out 

`classpath 'com.uber:okbuck:0.46.2'`

in the root build.gradle

Additionally, running `./gradlew app:dependencies` shows this dependency:

```
kotlinCompilerClasspath
\--- org.jetbrains.kotlin:kotlin-compiler-embeddable:1.3.0
     +--- org.jetbrains.kotlin:kotlin-stdlib:1.3.0
     |    +--- org.jetbrains.kotlin:kotlin-stdlib-common:1.3.0
     |    \--- org.jetbrains:annotations:13.0
     +--- org.jetbrains.kotlin:kotlin-script-runtime:1.3.0
     \--- org.jetbrains.kotlin:kotlin-reflect:1.3.0
          \--- org.jetbrains.kotlin:kotlin-stdlib:1.3.0 (*)
```

This changes when the okbuck plugin is added/removed
