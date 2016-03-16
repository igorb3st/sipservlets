![http://telestax.wpengine.netdna-cdn.com/wp-content/uploads/2014/06/alice_and_bob_video_call.jpg](http://telestax.wpengine.netdna-cdn.com/wp-content/uploads/2014/06/alice_and_bob_video_call.jpg)

# Introduction #

Mobicents SIP Servlets is bringing realtime communications (voice & video) to your Browser using HTML5 [WebRTC](http://webrtc.org) and [SIP Over WebSockets](http://tools.ietf.org/html/draft-ietf-sipcore-sip-websocket-04) ! See **[the Video of the Demo](http://vimeo.com/51744602) !**

The Mobicents HTML5 WebRTC Client allows you to make video calls from/to any Web Browser supporting [WebRTC](http://webrtc.org), ( (only Google Chrome Firefox and Opera supports it so far but some plugins exists to enable it on IE and Safari) as well as SIP Endpoints.

# Technology #

## Client Side ##

The [Client Side of the application](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fwebsocket-b2bua%2Fsrc%2Fmain%2Fsipapp%2Fjain-sip) was built using Twitter Boostrap for the UI, jQuery for the javascript interactions and [WebRTComm](http://code.google.com/p/webrtcomm/) for establishing the Call Sessions through [SIP Over WebSockets](http://tools.ietf.org/html/rfc7118).

## The Server Side ##

WebRTComm communicates with Mobicents SIP Servlets JAIN SIP Stack which supports [SIP Over WebSockets](http://tools.ietf.org/html/rfc7118). The [Server Side Application](http://code.google.com/p/sipservlets/source/browse/sip-servlets-examples/websocket-b2bua/src/main/java/org/mobicents/servlet/sip/example/WebSocketB2BUASipServlet.java) is a standard simple Back To Back User Agent that handles the SIP Over WebSockets Transport transparently and can bridge to any SIP EndPoint

# Requirements #

## Google Chrome 36+ and Firefox 22+ ##

WebRTC is enabled by default in Google Chrome, FireFox and Opera, so no specific setup is required, however since the release of Mobicents SIP Servlets 2.1.547, so make sure to use our latest releases from https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/

# Running the Example #

Install the latest version of Mobicents SIP Servlets and start it, [see our User Guide](https://mobicents.ci.cloudbees.com/job/Mobicents-SipServlets-Release/lastSuccessfulBuild/artifact/documentation/html_single/index.html#sssicar-SIP_Servlets_Server-Installing_Configuring_and_Running).

Be aware that you need to start Mobicents SIP Servlets on a network interface so that it is accessible from the network :

  * For JBoss AS 7, use ` $JBOSS_HOME/bin./standalone.sh -c standalone-sip.xml -b <ip_address> `

  * For Tomcat 7, modify the ` $CATALINA_HOME/conf/server.xml ` and change the connectors' IP Address attribute to your network IP Address

Once the Server is up and running, got to ` http://<ip_address>:8080/websockets-sip-servlet ` from one computer and register with the default name, then go to the same URL from the browser of a different computer (make sure the Requirements Section above is completed as well)
and register with a different user name (by example bob). Then it's like SKype. Type the name of your buddy in the input field (Add Room) and click on the + sign. Then click on the buddy you just added and start chatting or calling
You can follow instructions at http://www.telestax.com/livechat-and-video-call-with-restcomm/

# Screenshots and Live Demo #

## Live Video Call ##

[Live Video Call](https://www.facebook.com/photo.php?v=10151168634524654) from Brazil at Mobicents Summit 2012 in Rio with the Orange Labs team, the research and innovation centre of France Telecom-Orange, in France