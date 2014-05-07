# Branch oriented maven-dashboard-plugin 

Limitations of maven-dashboard-plugin 
-------------
maven-dashboard-plugin is a nice plugin that helps us to generate dashboard for our Maven project. Depending on branching strategy is can be perfect. However, for some companies it may be somewhat limited. Let's say that we have a group of developers working on bunch of features that are going to be released under the same version. In that case all statistics (e.g. CPD, PMD, Findbugs, etc.) are mixed. We are not sure which branch contributed to worse Findbugs results.

Requirements
-------------
Basically we wanted to track statistics for given branch (master, develop, etc.).
- When we insert results into DB they should be assigned either to given branch or not assigned to any branch (in that case the old logic should be applied).
- Charts that are being generated for given branch should present historical statistics either for given branch or all branches.
- It should be easy to configure.

Configuration
-------------
Everything what you need to do is to add branchName element to your configuration.
Let me show you how the configuration looks like in our case. We pass the branch name as a command line argument when running Maven and we are using passed value in the pom.xml.

```xml
<configuration>
	<configLocation>../some-parent/src/site/some-dashboard.xml</configLocation>
	<dialect>org.hibernate.dialect.DerbyDialect</dialect>
	<driverClass>org.apache.derby.jdbc.ClientDriver</driverClass>
	<connectionUrl>jdbc:derby://ciMachine.domain.com:1527/project;create=true</connectionUrl>
	<username>ciMachineUsername</username>
	<password>ciMachinePassword</password>
	<generateGraphs>true</generateGraphs>
	<m1LikeRendering>true</m1LikeRendering>
	<branchName>${ci_branch}</branchName>
</configuration>
```

http://mojo.codehaus.org/dashboard-maven-plugin/
