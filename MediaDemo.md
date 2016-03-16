# Service Description #

_Note : This application will only works on the Jboss container with the Mobicents Media Server 2.x installed on the Mobicents Sip Servlets for JBoss 5 version_

This simple example shows how Sip Servlets can leverage JSR-309 API which provides multimedia application developers with a generic media server (MS) abstraction interface.

JSR-309 defines a programming model and object model for MS control independent of MS control protocols.

Media Server Control API is not an API for a specific protocol.
It will take advantage of the multiple and evolving Multimedia Server (MS) capabilities available in the industry today and also provide an abstraction for commonly used application functions like multi party conferencing, multimedia mixing and interaction dialogs.

Some of the commonly used MS control protocols are MGCP (RFC 3435), MEGACO (RFC 3525), Media Server Markup Language (MSML) (RFC 4722) and VoiceXML.

The Mobicents implementation of JSR-309 API makes use of MGCP as MS control protocol. Look at bellow diagram for further understanding of
layers involved

![http://www.mobicents.org/SipJSR309.jpeg](http://www.mobicents.org/SipJSR309.jpeg)

In above diagram the Sip Phone (UA) interacts with Sip-Servlets Application deployed on Sip Servlets Server using the SIP messages and exchanges the SDP.

The Sip Servlets Application uses JSR-309 API which leverages MGCP to talk to Mobicents Media Server.

Once the hand-shake is done, the RTP flows between the UA and MMS.
This example demonstartes the Announcement, DTMF Detection and Recording capabilities of MMS.

The example is divided in 2 parts :

_Part I_

  1. Dial 1010 from you SIP Phone (or you can dial 1010tts to test the TTS version of the demo)
  1. You will hear an announcement (show casing the announcement capability)
  1. Dial a DTMF from your SIP Phone, the DTMF is recognized by the media-jsr309-servlet example and MS is instructed to play corresponding Announcement (show casing the DTMF detection capability of MS)

_Part II_

  1. Dial 1011 from your SIP Phone
  1. You will hear an announcement to start recording
  1. Once announcement is over, speak on your mic and your voice gets recorded to Mobicents Media Server Home directory (showcasing recording capability). After few seconds you can disconnect and manually go to Mobicents Media Server home directory and play test.wav using your favorite player.

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/media-jsr309-servlet/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/media-jsr309-servlet/media-jsr309-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/media-jsr309-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fmedia-jsr309-servlet)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

First you need to have Mobicents Media Server (MMS) up and running. Go to $JBOSS\_HOME/mobicents-media-server/bin and type sudo sh run.sh (sudo is needed because RTSP starts on port below 1024 which requires root privilege on linux) or run.bat on windows

Then start up Mobicents Sip Servlets.

Just dial the servlet directly as explained in below steps, without any proxy. Tested with Twinkle

  1. Dial 1010 to test Announcement and DTMF Detection
  1. Dial 1011 to test Recording