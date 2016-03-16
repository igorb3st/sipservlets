# Service Description #

When an INVITE is received, the Diameter Ro/Rf service checks if the caller has enough balance to establish the call, by sending an Diameter Credit-Control-Request with Cc-Request-Type AVP set to 'INITIAL\_REQUEST' to the Online Charging Server (OCS) to reserve initial units. If the user is not provisioned in the OCS or has insufficient funds, a 402 (Payment Required) message is sent back to the caller and the call is cancelled; if the user has enough funds to proceed, an initial amount of credit is reserved and the call establishment proceeds.

If the callee does not answer the call the reserved units are returned back to the OCS. If the call is answered and correctly established the actual call charging starts: the initially reserved units (10 by default, corresponding to 10 seconds) start being consumed. Once those units are consumed, a new Credit-Control-Request is sent to OCS with Cc-Request-Type AVP set to 'UPDATE\_REQUEST' in order to grant a new amount of units (10 by default). This is repeated whenever needed during the call.
Once the call is terminated, the amount of unused units are returned to the OCS by sending a Credit-Control-Request with Cc-Request-Type AVP set to 'TERMINATION\_REQUEST'. If the balance is exhausted before the user hangs up, the call is terminated by the Ro/Rf service.

The following scenarios for 3GPP TS 32.260 (Rel 9.10) are implemented in this example, with the S-CSCF being discarded for simplicity and the AS playing both roles:

![http://www.mobicents.org/diameter-ro-example-initiate.jpg](http://www.mobicents.org/diameter-ro-example-initiate.jpg)

![http://www.mobicents.org/diameter-ro-example-terminate.jpg](http://www.mobicents.org/diameter-ro-example-terminate.jpg)

# How to activate it #

## From the binary ##

Download the latest version of the war file corresponding to this example from [here](https://oss.sonatype.org/content/groups/public/org/mobicents/servlet/sip/examples/diameter-ro-rf/)

Drop the downloaded war file into your tomcat\_home/webapps directory or jboss\_home/server/default/deploy directory
Get the [corresponding dar configuration file](http://sipservlets.googlecode.com/git/sip-servlets-examples/diameter-ro-rf/diameter-ro-rf-servlet-dar.properties).

To understand what the dar configuration file is used for, check the Application Router Documentation .

Drop it in your tomcat\_home/conf/dars directory or jboss\_home/server/default/conf/dars directory.

To use this dar file for this service, specify in the Service xml tag, darConfigurationFileLocation attribute of the tomcat\_home/conf/server.xml file or jboss\_home/server/default/deploy/jboss-web.deployer/server.xml , the following :
conf/dars/diameter-ro-rf-servlet-dar.properties

You can now run your container (Tomcat or Jboss).

## From the source ##

Please check out the speed dial example located under [this location](http://code.google.com/p/sipservlets/source/browse/#git%2Fsip-servlets-examples%2Fdiameter-ro-rf)
from the svn repository. Just call mvn clean install war:inplace to create the war file in the target directory

# Configuration #

## MSS Client ##

Configure your Diameter client in  $JBOSS\_HOME/server/default/deploy/mobicents-diameter-mux-sar-jboss-5-`*`.FINAL.sar/config/jdiameter-config.xml under MSS with the following:

```
<?xml version="1.0"?>
<Configuration xmlns="http://www.jdiameter.org/jdiameter-server">

  <LocalPeer>
    <URI value="aaa://127.0.0.1:1812" />
    <IPAddresses>
      <IPAddress value="127.0.0.1" />
    </IPAddresses>
    <Realm value="mobicents.org" />
    <VendorID value="193" />
    <ProductName value="jDiameter" />
    <FirmwareRevision value="1" />
    <OverloadMonitor>
      <Entry index="1" lowThreshold="0.5" highThreshold="0.6">
        <ApplicationID>
          <VendorId value="193" />
          <AuthApplId value="0" />
          <AcctApplId value="19302" />
        </ApplicationID>
      </Entry>
    </OverloadMonitor>
  </LocalPeer>

  <Parameters>
    <AcceptUndefinedPeer value="true" />
    <DuplicateProtection value="true" />
    <DuplicateTimer value="240000" />
    <UseUriAsFqdn value="true" /> <!-- Needed for Ericsson Emulator (set to true) -->
    <QueueSize value="10000" />
    <MessageTimeOut value="60000" />
    <StopTimeOut value="10000" />
    <CeaTimeOut value="10000" />
    <IacTimeOut value="30000" />
    <DwaTimeOut value="10000" />
    <DpaTimeOut value="5000" />
    <RecTimeOut value="10000" />
  </Parameters>

  <Network>
    <Peers>
      <!-- Ro/Rf -->
      <Peer name="aaa://127.0.0.1:3868" attempt_connect="true" rating="1" />
    </Peers>

    <Realms>
      <!--  Ro/Rf -->
      <Realm name="mobicents.org" peers="127.0.0.1" local_action="LOCAL" dynamic="false" exp_time="1">
        <ApplicationID>
          <VendorId value="10415" />
          <AuthApplId value="4" />
          <AcctApplId value="0" />
        </ApplicationID>
      </Realm>
    </Realms>
  </Network>

  <Extensions />

</Configuration>
```

## Mobicents Diameter Charging Server Simulator ##

The server is already configured and ready to use. It will be running at port 3868 at IP address 127.0.0.1. The configuration can be changed by editing the file config-server.xml inside the Mobicents DCSS JAR.

The following account are provisioned by default:

  * sip:alexandre@mobicents.org (45 units)
  * sip:jderuelle@mobicents.org (123 units)

To add or change the provisioned accounts, please edit the file accounts.properties inside the Mobicents DCSS JAR, using the following format (the ':' needs to be escaped using a '\'):

```
sip\:<username>@<domain> = <units>
```

# How to play with it #

Download the Mobicents [Diameter Charging Server Simulator](http://mobicents.googlecode.com/files/mobicents-dcs.jar).

Configure it if needed and start it with java -jar <filename.jar>.
Run your container (JBoss AS).

Start two SIP Phones of your choice such as one of the accounts is provisioned at the Charging Server (eg: sip:alexandre@mobicents.org).
The SIP phones have to be registered.

From the provisioned account, make a call to the other phone. You can play with it by accepting the call and see the balance being deducted or cancelling/rejecting the call and see the balance being returned.