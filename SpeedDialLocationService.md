# Service Description #

This service is a composition of twos other services : Speed Dial and Location Service

The Speed Dial Service will proxy the speed dial number to a sip address, then the location service will proxies to the actual locations of the callee.

They will be invoked in this order Speed Dial then Location Service.

# How to activate it #

## From the binary ##

Download the latest version of the war files corresponding to the examples from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/speed-dial/) and [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/location-service/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/location-service/speeddial-locationservice-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/speed-dial-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fspeed-dial) and the the location service example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Flocation-service)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Start two SIP Phones.

One phone should be setup as sip:receiver@sip-servlets.com on ip address 127.0.0.1 and port 5090 .The other phone can be registered as anything,

The SIP phone doesn't have to be registered.

From the second phone, make a call to sip:1@sip-servlets.com you should have the "receiver" phone ringing.