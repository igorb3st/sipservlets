_You can play with most of our examples in 2 differents ways. From the binary or right from the source like a true hacker :-)
For testing against the examples you'll need to use some SIP softphones. We tested most of the examples with WengoPhone, 3CX VoIP Client, SJ Phone 1.65, Ekiga, linphone and XLite. Most of the examples uses the 5090 port for one of the SIP softphone to be contacted so please make sure, it is configured that way._

# Generic Examples #

Here is our list of examples that also helps us testing out our implementation, those examples will work on all versions of Mobicents Sip Servlets (Tomcat 7 and JBoss AS 7.x) :

  * [Call Blocking](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sfss-The_Call-Blocking_Service) : UAS application
  * [CallForwarding](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sfss-The_Call-Forwarding_Service) : B2BUA application
  * The two previous examples can be composed and become a new application known as [Call Controller](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sfss-The_Call-Controller_Service)
  * [Speed Dial](SpeedDial.md) : proxy application
  * [Location Service](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sfss-The_Location_Service) : proxy application
  * The two previous examples can be composed and become a new application showing what can be achieved with two [chained proxy applications](SpeedDialLocationService.md)
  * [Click to Call](Click2Call.md) : Converged application
  * [Chat Server](ChatServer.md) : support for sip extension MESSAGE

# Advanced Examples #

  * [Examples for Mobicents Sip Servlets on JBoss AS 7.x](MSSJBoss5Examples.md) only showcasing Media (JSR 309 based) and Diameter/IMS are also available

# Java EE6/Servlet 3.0 Examples #

Because they leverages unique features of Servlet 3.0 and Java EE 6 specifications, the examples below will work only on Mobicents Sip Servlets on Tomcat 7 or JBoss AS 7

  * [Click to Call Async Servlet 3.0](Click2CallAsync.md) : Revised the click to call application by integrating Servlet 3.0 Async features.