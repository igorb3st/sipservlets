# Service Description #

This simple example shows how SIP Servlets can be used along with HTTP servlets as a converged application to place calls from a web page. This example consists of the following steps:

  1. Alice and Bob each register a SIP Softphone
  1. Alice clicks on the "Call" link to place a call to Bob
  1. Alice's phone rings
  1. When Alice picks up her phone, Bob's phone rings
  1. When Bob answers his phone, the call is connected
  1. When one of them hangs up, the other one is also disconnected

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/click-to-call-servlet/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/click-to-call/click2call-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/speed-dial-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fclick-to-call)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Starts Two SIP phones.

Open up a browser to http://localhost:8080/click2call/.

If you have no registered SIp clients you will be asked to register at least two.

Configure your SIP clients to use the sip servlets server as a register and proxy. (ip address : 127.0.0.1, port: 5080)

After the registration you will see a table where each cell will initiate a call between the corresponding clients.

You can also navigate to http://localhost:8080/click2call/simplecall.html, which is a simplified version that doesn't require registered clients.

You will see the index page where you can enter two SIP URIs.

Enter the URIs of the two SIP phones you just started and click "Submit".
The SIP phones don't have to be registered.

After you pick up both phones the RTP session starts.