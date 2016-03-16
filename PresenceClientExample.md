# Service Description #

When receiving an INVITE request, the application will call out to the Mobicents SIP Presence Service to check if the from address is a blocked contact. If that's the case it sends out a FORBIDDEN in response and the processing stops.

![http://www.mobicents.org/mss-presence-client-example-fail.png](http://www.mobicents.org/mss-presence-client-example-fail.png)

If that's not the case it proxies the INVITE to the nex application in chain.

![http://www.mobicents.org/mss-presence-client-example-success.png](http://www.mobicents.org/mss-presence-client-example-success.png)

All configuration is taken from the sip.xml and used in the application to contact the XDMS for doing the user provisionning on application startup (create user and initial resource list creation) and then retrieving is the user taken from the From Header of the SIP INVITE is present in the blocked contacts of the user.

In a real world application, the users in the XDMS will be provisionned externally and the To Header of the SIP INVITE will be used to get the blocked list instead of using the default user from the sip.xml

This example is used in conjunction with the location service example as well to proxy the response to the correct location if the call is not blocked

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/call-blocking-presence/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/presence-client-example/presence-client-example-dar.properties.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/presence-client-example-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fpresence-client-example)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Download the lastest version of the [Mobicents SIP Presence XDMS Server](http://sourceforge.net/projects/mobicents/files/Mobicents%20SIP%20Presence%20Service/1.0.0.BETA6/mobicents-sip-presence-1.0.0.BETA6.zip/download). Extract it locally to a directory that we will reference as $MOBICENTS\_PRESENCE\_XDMS

Start it with the following command sh $MOBICENTS\_PRESENCE\_XDMS/bin/run.sh -Djboss.service.binding.set=ports-01
When the Mobicents XDMS Server is completely started, start Mobicents Sip Servlets with sh $MOBICENTS\_SIP\_SERVLETS/bin/run.sh

Start a SIP Phone of your choice such as the account name should be sip:blocked-sender@sip-servlets.com or sip:darth-vader@mobicents.org. The From Header should be one of the following addresses : sip:blocked-sender@sip-servlets.com or sip:darth-vader@mobicents.org.

Start another SIP Phone of your choice as the account name is sip:receiver@sip-servlets.com (as in the location service example ) on port 5090

The SIP phone doesn't have to be registered.
Make a call to sip:receiver@sip-servlets.com address, you should receive a Forbidden.

If you change the account name of the first SIP Phone the call will go through