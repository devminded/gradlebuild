# Gradle script plugin build (6.5.1)

## The problem

Sometimes Gradle seems to be built for the individual developer having most of the repositories, layout and paths hardcoded into the build files.
Working in a team in a company setting with heavy regulations, with a local access-controlled artifactory (mirror and for publishing) and the official mirrors blocked in the firewall we need a common init.gradle. I have a real problem with hardcoding URLs (which should be part of the environment and not the project) into buildscripts and then repeating the same URLs across 100s of different projects. I see this more and more and it seems to particularly prevalent in gradle/android app and nodejs development.

This init.gradle works just fine - for application dependencies - not so much for plugins (the included version is being kept simple for demonstrations purposes). In particular, splitting the build into separate script plugins (not buildSrc or modular build) we can't use the plugins{} section; we have to use "apply plugin" in each script and thus we also need to add the plugin to the classpath in a buildscript section for each script.

Well it still won't work. It works if I put everything in a single root build.gradle file in a plugins section and skip the classpath.

Why there is no easy way to provide plugin repositories and why we can't use a plugins section with a version in script plugins and why does it still complains about no repositories even after all this time is beyond me.

Either I don't know what I am doing or Gradle has forgotten about usability and the principle of least astonishment.

## The path to frustration

1. Move init/init.gradle to ~/.gradle/init.gradle
2. Run ./gradlew
3. Watch it fail
4. Become frustrated

```
Build file '.....\gradlebuild\build.gradle' line: 7

A problem occurred evaluating root project 'myapp'.
> Could not resolve all artifacts for configuration 'classpath'.
   > Cannot resolve external dependency com.bmuschko:gradle-docker-plugin:6.4.0 because no repositories are defined.
     Required by:
         unspecified:unspecified:unspecified
```
