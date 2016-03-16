# Service Description #

Speed Dial allows a calling party to specify a short speed-dial number (e.g. "1"), which it translates into a complete address based on prior configuration and proxies it (without record-routing, and without supervised mode).
Speed Dial currently performs a lookup into a hard coded list of addresses and should later evolve towards a database.
Here is the list of hard coded contacts and their locations :

  * "1" => "sip:receiver@sip-servlets.com"
  * "2" => "sip:mranga@sip-servlets.com" (The Master Blaster)
  * "3" => "sip:vlad@sip-servlets.com"
  * "4" => "sip:bartek@sip-servlets.com"
  * "5" => "sip:jeand@sip-servlets.com"
  * "9" => "sip:receiver@127.0.0.1:5090" (Special case to be able to run the app standalone)

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/speed-dial/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/speed-dial/speed-dial-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/speed-dial-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fspeed-dial)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Start two SIP Phones.

One phone should be setup as sip:receiver@sip-servlets.com on ip address 127.0.0.1 and port 5090 The other phone can be registered as anything
The SIP phone doesn't have to be registered.

From the second phone, make a call to sip:9@sip-servlets.com you should have the "receiver" phone ringing.