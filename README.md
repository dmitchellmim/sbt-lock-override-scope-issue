# sbt-lock dependencyOverrides scope issue

[According to sbt documentation](https://www.scala-sbt.org/1.x/docs/Library-Management.html#Overriding+a+version), you can use `show update` to verify that sbt chooses the versions specified by `dependencyOverrides`. However, scoping as `dependencyOverrides in Compile` causes the override to be ignored.

`build.sbt` excerpt:
```sbt
libraryDependencies += "org.jooq" % "jooq" % "3.14.0"
```

`lock.sbt` excerpt:
```sbt
dependencyOverrides in Compile ++= {
      "org.jooq" % "jooq" % "3.13.0"
  }
}
```

`show update` excerpt (it resolved 3.14.0 from `libraryDependencies`, not 3.13.0 from `dependencyOverrides`):
```
[info] Update report:
[info]      compile:
[info]            org.jooq:jooq:3.14.0:default: (Artifact(jooq, jar, jar, None, Vector(), Some(https://repo1.maven.org/maven2/org/jooq/jooq/3.14.0/jooq-3.14.0.jar), Map(), None, false),/Users/dmitchell/Library/Caches/Coursier/v1/https/repo1.maven.org/maven2/org/jooq/jooq/3.14.0/jooq-3.14.0.jar)
```