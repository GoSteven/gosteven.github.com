---
layout: post
title: "maven effective pom"
date: 2014-05-07 05:50
comments: true
categories: maven
---

maven-plugin-plugin version bugged me for a day. The build plugin is not specified anywhere in our poms, so there is a default version set in maven itself somewhere.

Running `mvn help:effective-pom` to get the "effective" pom. Maven 3.0.4 gives 2.9 and 3.2 gives 3.2.

Effective POM is composed of Super POM + Application POM(s) + settings.xml contents + plugins bound to the lifecycle. The defult bindings is in maven-core-\*.jar:META-INF/plexus/components.xml.

In the last, it is always a good practice to lock the version for everything. There is also a Maven Enforcer Plugin and its Require Plugin Versions rule to enforce this practice (which means the build will fail if you don't lock down plugins versions).
