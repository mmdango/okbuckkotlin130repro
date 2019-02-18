Problem:

Okbuck looks for wrong artifact ID with androidx libraries when using `forcedOkbuck` on certain Play Services libraries.

To repro:

run `./buckw` to invoke okbuck:

and observe:

```
* What went wrong:
Execution failed for task ':app:okbuck'.
> Could not resolve all artifacts for configuration ':app:debugRuntimeClasspath'.
   > Could not find support-v4.aar (androidx.legacy:legacy-support-v4:1.0.0).
     Searched in the following locations:
         https://dl.google.com/dl/android/maven2/androidx/legacy/legacy-support-v4/1.0.0/support-v4-1.0.0.aar

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org
```

Okbuck is looking for `support-v4.aar` instead of `legacy-support-v4.aar`.

When I remove the `forcedOkbuck` line, it works as expected.