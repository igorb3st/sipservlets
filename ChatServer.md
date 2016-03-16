# Service Description #

A chat server is a virtual location where many instant messenger applications can talk to each other.

Messages that arrive in a chat room are broadcast to all other people in the room. In other words, all messages are seen by all users. This means when a message arrives at our server application, the user's address will be added to a list. Then the message will be sent to all users in that list.

Additionally, you could implement "commands." A command begins with a forward slash (/) and is not broadcast, but instead is processed by the server itself for special features. The commands implemented are:

  * /join: Silently enter a chat room without broadcasting anything.
  * /who: Print the list of all users in this chat room.
  * /quit: Leave the chat room; no more messages will come in.

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/chatroom-servlet/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/chatserver/dar-chatserver.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/speed-dial-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fchatserver)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Starts Two sip phones.

Starts Two SIP Chat Clients. Point them to sip:just4fun@127.0.0.1:5080

Type your message and then click on the send button

You should see the messages in both clients once they are both in the chat server (that is when they sent at least one message to it).