# Service Description #

Application that can be used to alert a phone number that an event has occured.

This application was developped so that the [JBoss RHQ/Jopr Enterprise Management Solution](http://www.jopr.org/) would be able to notify system administrators when a monitoring alert is fired by Jopr/RHQ

More information can be found on [heiko's blog](http://pilhuhn.blogspot.com/2009/09/jopr-talking.html) or on the following [online presentation](https://docs.google.com/present/edit?id=0AXZ3Uhj-XHcDZGZjanI0OHpfMTg1aGZ3c3EzZHE&hl=en)

The intent is to have multiple communication channels to alert people through Twitter, SMS, Phone calls, XMPP etc...

So the application features one context path per communication channel :

  * SMS is on http://host :port /alerting-app/sms : an SMS is send to the phone number

  * Phone calls is on http://host :port /alerting-app/sms : a Phone call is placed to the phone number and the callee can give feedback by pressing phone buttons

Each Servlet for a Communication Channel takes the mandatory following arguments :

  * alertId : the id of the alert (by example 12345)
  * tel : the phone number you want to dial ( by example sip:mobicents@127.0.0.1:5060 for a SIP Phone or sip:+33679797979@callwithus.com for a phone call going through the callwithus VoIP provider)
  * alertText : the text of the alert (by example Server 1 on Cluster Mobicents is overloaded, press 1 to restart, press 2 to stop...)

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/alerting-app/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/alerting-app/alerting-app-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/alerting-app-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fclick-to-call)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# How to play with it #

Depending on which alert you want to try hit one of the following test pages :

  * SMS : http://localhost:8080/alerting-app/send-sms-alert-test.html (you will need to open an account with Esendex and modify the web.xml to enter your credentials)
  * Phone calls : http://localhost:8080/alerting-app/send-alert-test.html (if you need to call out to a real phone you will need to open an account with Call With Us or an online VoIP"provider and modify the web.xml to enter your credentials)