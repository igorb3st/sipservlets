_The purpose here is to demonstrate integration with more technologies and protocols than just SIP and HTTP.
It is a Converged JEE Application showing SEAM & JEE integration and Media integration with TTS and DTMF support.
This application only works on a full JEE Container, in other words it will only work on top of Jboss AS and not Tomcat._

_The idea is to have a converged application that shows how JEE application can leverage Sip Servlets to have voice, message and data transfer seamlessly.  This example is built using Seam, Mobicents Sip Servlets and Mobicents Media Server deployed on JBoss AS._

# Service Description #

Once User places an order, he/she receives call to confirm for the same.

User presses 1 and order state remains as OPEN and flow continues.

If User presses 2 order gets CANCELLED and flow completes

If order is less than 100$ it gets approved automatically as per the rule set by jBPM and User receives call to set delivery date and time.

If order is greater than 100$, Admin has to either approve or reject the order.

If Admin doesn't log on the site and take necessary action, call is initiated to Admin and Admin preses DTMF to take necessary action
Admin presses 1 and order state changes to PROCESSING and flow continues.

If Admin presses 2 order gets CANCELLED and flow completes.
User id for Admin is 'manager' and password is 'password'
Once order is approved by Admin, a call is initiated to User to set the date and time for delivery

Please note that for orders greater than 100$ call to User to set delivery date and time is only initiated if Admin logs on to system and approves. This is because the logic is tied with jBPM process and it hasn't been yet taken care of in the application.

User sets delivery date and time by punching numbers on his/her phone. As soon as this is done user can see the delivery date and time set on 'My Orders' tab and click on 'Show Details' for corresponding order.
Once again the ball roles on to Admin, and he/she has to log in the site and mark the order for Shipping

As soon as Admin marks the order for Shipping, call is initiated to User to remind him/her date and time when the shipment will arrive.


# How to activate it #

## From the binary ##

Download the latest version of the EAR file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/shopping-demo-ear-jsr309/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/shopping-demo-jsr309/shopping-demo-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/shopping-demo-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fshopping-demo-jsr309)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Make sure you have the Media Server running. It has it's own bin/run.sh script.

http://localhost:8080/shopping-demo/

Start a Sip Phone, make it register as a customer (let's say sip:jean@shopping-demo.com) to your Jboss AS SIP Connector listening point (default to 127.0.0.1:5080).

Start another Sip Phone, make it register as admin (if you're using the binary or if you didn't change the sip.xml file it should be sip:admin@shopping-demo.com) to your Jboss AS SIP Connector listening point (default to 127.0.0.1:5080).

Before shopping create a new account and make sure that you enter the SIP address for Phone field of your registered Sip Phone (here sip:jean@shopping-demo.com).

Note: The new account created won't survive server restart. If you want it to survive server restart, it requires you to modify import.sql which is stored under "ShoppingDemo.ear/ShoppingDemo.jar". This is because the SIP phone addresses for all the users (user1,user2 etc...) are hardcoded here and we are using an in-memory database called HSQLDB that is created and dropped on every restart. If you SIP client address is different, this is where you would modify it. To make this easy you can explode the ear under deploy directory and also explode the jar under the ear. That way you can easily modify the import.sql.

For SIP Phone settings you can see examples at SIP Phone Settings for Converged Demo

After creation of account once you check out the cart a call will be received on the customer SIP Phone for confirmation.

You can check your Order Status via 'My Orders' tab

After 30000 milli secs ( value specified for order.approval.waitingtime in convergeddemo.properties) call is received by Admin to confirm the order for Shipping or Cancel if order is greater than 100$ or a call will be received on the customer sip phone for choosing delivery date if order is lower than 100$

You can check log out and relog in as manager to accept the order if it is greater than 100$, then a call will be received on the customer sip phone for choosing delivery date. You can also ship the orders that have been accepted and then a reminder call will be placed on the customer sip phone.