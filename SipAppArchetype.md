# Creating the Hello SIP World Project #

To create your SIP Servlets application

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-sipapp -DarchetypeGroupId=org.mobicents.servlet.sip.archetypes -DarchetypeArtifactId=maven-archetype-sipapp -DarchetypeVersion=1.1
```

this should give a similar output to the one below

```
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> maven-archetype-plugin:2.2:generate (default-cli) @ standalone-pom >>>
[INFO] 
[INFO] <<< maven-archetype-plugin:2.2:generate (default-cli) @ standalone-pom <<<
[INFO] 
[INFO] --- maven-archetype-plugin:2.2:generate (default-cli) @ standalone-pom ---
[INFO] Generating project in Interactive mode
[INFO] Archetype repository missing. Using the one from [org.mobicents.servlet.sip.archetypes:maven-archetype-sipapp:1.1] found in catalog local
Downloading: http://repo.maven.apache.org/maven2/org/mobicents/servlet/sip/archetypes/maven-archetype-sipapp/1.1/maven-archetype-sipapp-1.1.jar
Downloaded: http://repo.maven.apache.org/maven2/org/mobicents/servlet/sip/archetypes/maven-archetype-sipapp/1.1/maven-archetype-sipapp-1.1.jar (5 KB at 9.1 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/mobicents/servlet/sip/archetypes/maven-archetype-sipapp/1.1/maven-archetype-sipapp-1.1.pom
Downloaded: http://repo.maven.apache.org/maven2/org/mobicents/servlet/sip/archetypes/maven-archetype-sipapp/1.1/maven-archetype-sipapp-1.1.pom (8 KB at 16.1 KB/sec)
[INFO] Using property: groupId = com.mycompany.app
[INFO] Using property: artifactId = my-sipapp
Define value for property 'version':  1.0-SNAPSHOT: : 
[INFO] Using property: package = com.mycompany.app
Confirm properties configuration:
groupId: com.mycompany.app
artifactId: my-sipapp
version: 1.0-SNAPSHOT
package: com.mycompany.app
 Y: : 
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: maven-archetype-sipapp:1.1
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: com.mycompany.app
[INFO] Parameter: artifactId, Value: my-sipapp
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: com.mycompany.app
[INFO] Parameter: packageInPathFormat, Value: com/mycompany/app
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: com.mycompany.app
[INFO] Parameter: groupId, Value: com.mycompany.app
[INFO] Parameter: artifactId, Value: my-sipapp
[INFO] project created from Archetype in dir: /temp/applications
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 12.290s
[INFO] Finished at: Tue May 01 17:09:58 CEST 2012
[INFO] Final Memory: 8M/91M
[INFO] ------------------------------------------------------------------------
```

Once the Maven Archetype plugin creates the project, change directories into the my-sipapp directory and take a look at the pom.xml. You should see the **Initial POM for the my-sipapp Project**.

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-sipapp</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>my-sipapp Maven SipApp</name>
  <url>https://code.google.com/p/sipservlets/</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <!-- logging dependency -->
		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>1.2.14</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>commons-logging</groupId>
			<artifactId>commons-logging-api</artifactId>
			<version>1.0.4</version>
			<scope>provided</scope>
		</dependency>

		<!-- web j2ee dependencies -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<version>2.5</version>
			<scope>provided</scope>
		</dependency>
		<!-- sip dependencies -->
		<dependency>
			<groupId>org.mobicents.servlet.sip</groupId>
			<artifactId>sip-servlets-spec</artifactId>
			<version>1.7.0.FINAL</version>
			<scope>provided</scope>
		</dependency>

  </dependencies>
	<build>
		<finalName>my-sipapp</finalName>
		<plugins>
			<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>2.4</version>
				<configuration>
					<source>1.6</source>
					<target>1.6</target>
				</configuration>
			</plugin>
			<plugin>
				<artifactId>maven-war-plugin</artifactId>
				<version>2.2</version>
				<configuration>
					<failOnMissingWebXml>false</failOnMissingWebXml>
                                        <warSourceDirectory>${basedir}/src/main/sipapp</warSourceDirectory>
				</configuration>
			</plugin>
		</plugins>		
	</build>
	<!-- repositories -->
	<repositories>
		<repository>
			  <id>mobicents-public-repository-group</id>
			  <name>Mobicens Public Maven Repository Group</name>
			  <url>https://oss.sonatype.org/content/groups/public</url>
			  <layout>default</layout>
			  <releases>
			    <updatePolicy>never</updatePolicy>
			  </releases>
			  <snapshots>
			    <updatePolicy>never</updatePolicy>
			  </snapshots>
		</repository>
		<repository>
			<id>jboss-public-repository-group</id>
			<name>JBoss Public Maven Repository Group</name>
			<url>https://repository.jboss.org/nexus/content/groups/public/</url>
			<layout>default</layout>
			<releases>
				<updatePolicy>never</updatePolicy>
			</releases>
			<snapshots>
				<updatePolicy>never</updatePolicy>
			</snapshots>
		</repository>	 
	</repositories>
</project>
```

Notice the packaging element contains the value war. This packaging type is what configures Maven to produce a web application archive in a WAR file. A project with war packaging is going to create a WAR file in the target/ directory. The default name of this file is ${artifactId}-${version}.war. In this project, the default WAR would be generated in target/my-sipapp-1.0-SNAPSHOT.war. In the my-sipapp project, we’ve customized the name of the generated WAR file by adding a finalName element inside of this project’s build configuration. With a finalName of my-sipapp, the package phase produces a WAR file in target/my-sipapp.war.

# Deploying to Mobicents #

[Install Mobicents as described in the User Guide](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sssicar-SIP_Servlets_Server-Installing_Configuring_and_Running)

and deploy your application in either $TOMCAT\_HOME/webapps or $JBOSS\_HOME/server/default/deploy and copy over the my-sipapp/dar/mobicents-dar.properties to the $TOMCAT\_HOME/conf/dars or $JBOSS\_HOME/server/default/conf/dars/mobicents-dar.properties

You can now start the container and make a call using your favorite SIP Client

_Please note the call will probably be terminated right away since this example doesn't handle the Media Part and usually SIP Clients terminate the call if the media path can't be established_


# Troubleshooting #

In case a new version of the maven sipapp archetype has been recently released and is not yet synched to the Maven Central Repository, the oss.sonatype.org maven repository has to be added to the maven global configuration to be able to fetch the archetype. This is achieved by adding the following profile to your M2\_HOME/conf/settings.xml

```
<profile>
  <id>maven-archectype-sipapp</id>
  <repositories>
    <repository>
      <id>mobicents-public-repository-group</id>
      <name>Mobicens Public Maven Repository Group</name>
      <url>https://oss.sonatype.org/content/groups/public</url>
      <layout>default</layout>
      <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
      </snapshots>
    </repository>
  </repositories>
  <pluginRepositories>
    <pluginRepository>
      <id>mobicents-public-repository-group</id>
      <name>Mobicens Public Maven Repository Group</name>
      <url>https://oss.sonatype.org/content/groups/public</url>
      <layout>default</layout>
      <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
      </snapshots>
    </pluginRepository>
  </pluginRepositories>
</profile>
```

and the profile should be added mentioned above to create the application
```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-sipapp -DarchetypeGroupId=org.mobicents.servlet.sip.archetypes -DarchetypeArtifactId=maven-archetype-sipapp -DarchetypeVersion=1.1 -P maven-archectype-sipapp
```