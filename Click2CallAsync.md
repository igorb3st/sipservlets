# Servlet 3.0 benefits #

Tomcat 7 and JBoss AS 7 implements the fresh Java Servlets 3.0 spec which among others brings two significant features, the asynchronous processing of requests and a new set of annotations, to add on top of the existing annotations, that can be used to define a web servlet, thus make the web.xml deployment descriptor optional (Sip Servlets 1.1 - JSR 289 already provides a set of annotations that can be used in order to define a sip servlet, so make optional the sip.xml deployment descriptor also).

The values of asynchronous processing of requests in a converged HTTP/SIP application are tremendous. Having asynchronous processing in the game, there is no need to send an HTTP request in order for the UI to get updated, this can happen every time a new SIP message arrives.

Any action initiated by the sip endpoint will update the web application and vice versa. For example, when a new user registers, the REGISTER message will update the page to display the new user, and when the client clicks to call this new user, the sip endpoint will start ringing and so on.

A converged application will now be able to follow, present and react almost in real-time on every event that initiated from or destined to the HTTP/SIP Servlet container by any client, either a sip endpoint or a web browser.

Important for the performance of the server is the fact that since there is no request being sent in order to update the UI, there is a low-lag communication thus no waste of server resources or network bandwidth, which is especially valuable when there are multiple clients.

Combined the previous features together, we can have a converged HTTP/SIP application with no deployment descriptors and asynchronous request processing, or in other words, Server Push, and here its the new, modern, version of the traditional click-to-call example to present in action these features.

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

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/click-to-call-servlet3.0/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/click-to-call-servlet3/click2call-async-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/speed-dial-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fclick-to-call-servlet3)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Starts Two SIP phones.

Open up a browser to http://localhost:8080/Click2CallAsync/.

If you have no registered SIP clients you will be asked to register at least two.

Configure your SIP clients to use the sip servlets server as a register and proxy. (ip address : 127.0.0.1, port: 5080)

By default it will accept any password, see below for instructions on how to enable security and authentication.  After the registration you will see a table where each cell will initiate a call between the corresponding clients.

After you pick up both phones the RTP session starts.