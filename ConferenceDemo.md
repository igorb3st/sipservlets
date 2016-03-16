# Service Description #

This example is focusing on the interaction with the more advanced features in Mobicents Media Server - endpoint composition and conferencing.

It is using the [Google's GWT Ajax framework](https://developers.google.com/web-toolkit/) with [server-push updates](http://code.google.com/p/google-web-toolkit-incubator/wiki/ServerPushFAQ) (a.k.a "reverse Ajax" or Comet) to provide desktop-like experience for the user interface.

The application is demonstrating how Sip Servlets can work seamlessly with any third-party web framework without repackaging or modifying the deployment descriptors.

All that is needed are a two Java annotations in the code to specify the application name and the servlet name, nothing else.

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/conference-demo-jsr309/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/conference-demo-jsr309/conference-demo-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/conference-demo-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fconference-demo-jsr309)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Once the application is deployed it is ready to serve requests. You can navigate to the [application homepage](http://localhost:8080/conference-demo-<version>) to observe the conference status. There are two way to join the conference:

  1. You can dial "sip-servlets-conference@localhost:5080" from a SIP Phone in order to join the conference.
  1. You can dial a SIP Phone from the form in the web application.
Additionally once the conference is started you can play an announcement by typing a file name in the respective text-box and pressing "Play file". The file must be PCM, mono, 16 bits, 8KHz WAV.
Participants can be muted and unmuted at any time.