
```java
java.lang.NoSuchMethodError: org.junit.runner.Request.classWithoutSuiteMethod(Ljava/lang/Class;)Lorg/junit/runner/Request;
    at org.eclipse.jdt.internal.junit4.runner.JUnit4TestMethodReference.createRequest(JUnit4TestMethodReference.java:31)
    at org.eclipse.jdt.internal.junit4.runner.JUnit4TestMethodReference.<init>(JUnit4TestMethodReference.java:25)
    at org.eclipse.jdt.internal.junit4.runner.JUnit4TestLoader.createTest(JUnit4TestLoader.java:54)
    at org.eclipse.jdt.internal.junit4.runner.JUnit4TestLoader.loadTests(JUnit4TestLoader.java:38)
    at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:452)
    at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:683)
    at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.run(RemoteTestRunner.java:390)
    at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.main(RemoteTestRunner.java:197)
```

这是JUnit4早期版本存在的BUG；更新JUnit版本为4.4+即可。