# Introduction #

This section explains, for people interested in contributing to Mobicents Sip Servlets, how to to setup the IDE. We currently supports only Eclipse. Although if you're willing to help contributing support for other IDEs, we would gladly welcome that

# Prerequisites #

Checkout the Mobicents sip servlets project from the source as described in the [Source Page](http://code.google.com/p/sipservlets/source/checkout)

Set up the environment variable CATALINA\_HOME and make it the same as your tomcat root installation by example E:\servers\apache-tomcat-6.0.35 or Set up the environment variable JBOSS\_HOME and make it the same as your tomcat root installation by example E:\servers\jboss-7.1.1.FINAL depending on which server you want to deploy to

From the command line and within the newly created mobicents-sip-servlets directory call

```
mvn clean install
```

or

```
mvn clean install -P as7
```

if you want to deploy to AS7. You can check all the profiles in the [root pom](http://code.google.com/p/sipservlets/source/browse/pom.xml#198).

# Eclipse Setup #

Start your Eclipse 3.7 and create a mobicents-sip-servlets workspace (you can create wherever you want even make it point to the newly created mobicents-sip-servlets directory)

Now you'll need to create the M2\_REPO variable so that Eclipse can locate the dependencies jar files.

To do that click on the 'Window' menu, then Preferences. On the popup, click on Java->Build Path->ClassPath variables as shown in the screenshot below

![http://www.mobicents.org/mss-eclipse-variables.png](http://www.mobicents.org/mss-eclipse-variables.png)

You'll need to create the M2\_REPO variable by clicking the new button in the popup.
Then fill out the input text fields with Name = M2\_REPO and Value = "the location of your maven 2 repository" (which is usually located at on your filesystem at "your user directory"/.m2/repository) Then click the OK button as shown on the sreenshot below

![http://www.mobicents.org/mss-eclipse-m2-variable.png](http://www.mobicents.org/mss-eclipse-m2-variable.png)

All the eclipse metadata information is already present in the svn trunk so you'll just need to import the different projects and that should work out of the box
Now click on File->Import then in the popup click on General->Existing projects into workspace and click on Next as shown in the screenshot below

![http://www.mobicents.org/mss-eclipse-import.png](http://www.mobicents.org/mss-eclipse-import.png)

In the new screen of the popup, click on the Browse button and select the mobicents-sip-servlets directory (that has been created by the svn checkout) and import all the projects (except the www-sip-servlets project) as shown in the screenshot below

![http://www.mobicents.org/mss-eclipse-projects.png](http://www.mobicents.org/mss-eclipse-projects.png)

And in the screenshot below is the final result of the newly created mobicents-sip-servlets Eclipse workspace. You're now ready to contribute to Mobicents Sip Servlets ! :-)

![http://www.mobicents.org/mss-eclipse-setup.png](http://www.mobicents.org/mss-eclipse-setup.png)