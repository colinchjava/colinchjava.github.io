---
layout: post
title: "How to set Java PATH and CLASSPATH in a Jenkins job"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

When running a Jenkins job that requires Java, it is important to ensure that the correct Java PATH and CLASSPATH are set. This allows Jenkins to locate the Java executable and necessary libraries required for the job to run successfully.

### Setting Java PATH in a Jenkins Job

To set the Java PATH in a Jenkins job, follow these steps:

1. Open the Jenkins job configuration page for the desired job.

2. Scroll down to the "Build Environment" section and check the "Set up JDK" option. This will display additional configuration options.

3. Select the desired JDK version from the "JDK" dropdown menu. If the required JDK is not listed, you may need to configure it in the Jenkins global configuration settings.

4. Optionally, you can check the "Auto install JDK" option to automatically install the selected JDK if it is not already available on the Jenkins machine.

5. Save the job configuration to apply the changes.

With these steps, Jenkins will automatically set the Java PATH based on the configured JDK in the job.

### Setting Java CLASSPATH in a Jenkins Job

To set the Java CLASSPATH in a Jenkins job, you can either set it directly in the build script or configure it in the Jenkins job settings.

#### Setting CLASSPATH in a Build Script

If you prefer to set the Java CLASSPATH directly in the build script, you can use the `export` command (Unix/Linux) or the `set` command (Windows) to set the CLASSPATH variable with the desired paths.

For example, in a Unix/Linux shell:

```sh
export CLASSPATH=/path/to/library.jar:/path/to/another_library.jar
```

And in a Windows batch script:

```bat
set CLASSPATH=C:\path\to\library.jar;C:\path\to\another_library.jar
```

Make sure to adjust the paths to match your actual library locations.

#### Setting CLASSPATH in Jenkins Job Settings

To set the Java CLASSPATH in a Jenkins job, follow these steps:

1. Open the Jenkins job configuration page.

2. Scroll down to the "Build" section and locate the "Add build step" dropdown menu.

3. Select the appropriate build step for your job, such as "Execute shell" for Unix/Linux or "Execute Windows batch command" for Windows.

4. In the build step configuration, type the command to set the CLASSPATH variable using the `export` command (Unix/Linux) or `set` command (Windows), followed by the desired paths.

5. Save the job configuration to apply the changes.

For example, in a Unix/Linux shell build step:

```sh
export CLASSPATH=/path/to/library.jar:/path/to/another_library.jar
```

And in a Windows batch script build step:

```bat
set CLASSPATH=C:\path\to\library.jar;C:\path\to\another_library.jar
```

Remember to adjust the paths to match your specific library locations.

By following these steps, you can ensure that the Java PATH and CLASSPATH are properly set in a Jenkins job, enabling the successful execution of the job that relies on Java.