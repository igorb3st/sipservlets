# Service Description #

Diameter Event Charging service based on Location Service that performs call charging at a fixed-rate (event charging). When the call is initiated there's a debit of 10.0 euros. In case of the call being rejected or the caller hangs up before an answer is received, that value is refunded into the user account.

The steps performed by the application and container are as follows:

  * Alice makes a call to sip:receiver@sip-servlets.com. The INVITE is received by the servlet container **which sends the debit request to the Charging Server** and invokes the location service
  * The location service determines, using non-SIP means, where the callee (receiver) is registered with two locations, identified by, say, two SIP URIs (sip:receiver@127.0.0.1:5090 and sip:receiver@127.0.0.1:6090).
  * The service proxies to those two destinations in parallel, without record-routing, and without the supervised mode.
  * Once one of the destinations return 200 (OK), the other branch is cancelled by the container.
  * The 200 is forwarded upstream to Alice and the call setup is completed as per usual.
  * **If none of the destinations accepts the call, a Diameter Accounting-Request for refund is sent to the Diameter Charging Server in order to credit the 10.0 euros debited.**


# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/diameter-event-charging/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/diameter-event-charging/diametereventcharging-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/diametereventcharging-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fdiameter-event-charging)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

This example must be run under JBoss.

You will also need [Ericsson SDK Charging Emulator v1.0](http://mobicents.googlecode.com/files/ChargingSDK-1_0_D31E.zip).

Run the Charging Emulator (PPSDiamEmul.jar) and configure it like this:

Peer Id: aaa://127.0.0.1:21812
Realm: mobicents.org
Host IP: 127.0.0.1

![http://www.mobicents.org/config_options.png](http://www.mobicents.org/config_options.png)

Start two SIP Phones.

One phone should be setup as sip:receiver@sip-servlets.com on ip address 127.0.0.1 and port 5090

The other phone can be setup as anything.

The SIP phone doesn't have to be registered.

We recommend using Linphone, Twinkle or WengoPhone.

From the second phone, make a call to sip:receiver@sip-servlets.com you should have the other phone ringing.

You should see there is one first request, right after the invite and before the other party accept/reject the call, sent to the Charging Emulator, that's when the debit is made. In case the call is rejected, or the caller gives up, there's a new Diameter Request sent which will be the refund of the unused value. In case the call is accepted, nothing else will happen, related to Diameter.

You can see the user balance in the emulator: in the menu Config > Account > Click on "00001000-Klas Svensson" and watch the balance. Stretch the window down to see the history.

![http://www.mobicents.org/config_account.png](http://www.mobicents.org/config_account.png)

Please note that this is not the most correct way to do charging, as Diameter provides other means such as unit reservation, but only as purpose of a demo, where you can see debit and refund working. Also, this is a fixed price call, no matter what the duration. You can also have it using time-based charging.