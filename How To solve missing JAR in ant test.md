## How to solve "Cause: the class org.apache.tools.ant.taskdefs.optional.junit.JUnitTask was not found." while running "ant test"?
```sh
BUILD FAILED
/var/lib/jenkins/workspace/First_pipeline_project/Unit Test Pipeline/test.xml:31: Problem: failed to create task or type junit
Cause: the class org.apache.tools.ant.taskdefs.optional.junit.JUnitTask was not found.
        This looks like one of Ant's optional components.
Action: Check that the appropriate optional JAR exists in
        -/usr/share/ant/lib
        -/var/lib/jenkins/.ant/lib
        -a directory added on the command line with the -lib argument

Do not panic, this is a common problem.
The commonest cause is a missing JAR.

This is not a bug; it is a configuration problem

	at org.apache.tools.ant.UnknownElement.getNotFoundException(UnknownElement.java:499)
	at org.apache.tools.ant.UnknownElement.makeObject(UnknownElement.java:431)
	at org.apache.tools.ant.UnknownElement.maybeConfigure(UnknownElement.java:163)
	at org.apache.tools.ant.Task.perform(Task.java:347)
	at org.apache.tools.ant.Target.execute(Target.java:435)
	at org.apache.tools.ant.Target.performTasks(Target.java:456)
	at org.apache.tools.ant.Project.executeSortedTargets(Project.java:1393)
	at org.apache.tools.ant.Project.executeTarget(Project.java:1364)
	at org.apache.tools.ant.helper.DefaultExecutor.executeTargets(DefaultExecutor.java:41)
	at org.apache.tools.ant.Project.executeTargets(Project.java:1248)
	at org.apache.tools.ant.Main.runBuild(Main.java:851)
	at org.apache.tools.ant.Main.startAnt(Main.java:235)
	at org.apache.tools.ant.launch.Launcher.run(Launcher.java:280)
	at org.apache.tools.ant.launch.Launcher.main(Launcher.java:109)
  ```
  
 ## Solutions 
 1. Install java 1.8.0
 ```sh 
 $ sudo yum install java 1.8.0 openjdk devel
 ```
 2. using Mint, based on Debian
 ```sh
 $ sudo apt-get install ant-optional
 ```
 3. RHEL-based systems once ant-junit was installed:
  ```sh
  $ sudo yum install ant-junit
  ```
