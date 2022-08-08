# Setting-MTU
Setting-MTU


Setting the MTU on Windows hosts 

1) check for what interfaces there are already

netsh interface ipv4 show subinterface 

2) find the interface you are interested in 

check the output in the table: 
C:\Users\Me\> netsh interface show subinterface

MTU   MediaSenseState  BytesIN  BytesOut          Interface 
------  -------------    ------   ------          ----------
xxxxxx        1             0           54535    Loopback Pseudo-Interface  
1500          1             2324343       23423232 Wi-Fi                 (On Dell it's Wi-Fi, on HP it's WiFi )
1500          5              0           0        Ethernet
1500          5              0           0        Local Area Connection* 1 
1500          5              0           0        Bluetooth Network Connection 


Note need to me Admin user to set the MTU: 

3) set the MTU for each interface you need to 

C:\Windows\System32\> netsh interface ipv4 set subinterface "Wi-Fi" mtu=1420 store=persistent 
Ok!                     << Message returned when set correctly 

C:\Windows\System32\> netsh interface ipv4 set subinterface "Ethernet" mtu=1420 store=persistent 
Ok!                     << Message returned when set correctly 
check it's set


check the output in the table: 
C:\Users\Me\> netsh interface show subinterface

MTU   MediaSenseState  BytesIN  BytesOut          Interface 
------  -------------    ------   ------          ----------
xxxxxx        1             0           54535    Loopback Pseudo-Interface  
1420          1             2324533       23425332 Wi-Fi                 (On Dell it's Wi-Fi, on HP it's WiFi )
1420          5              0           0        Ethernet
1500          5              0           0        Local Area Connection* 1 
1500          5              0           0        Bluetooth Network Connection 


Note turn off IPV6 as well so that the traffic has to follow the IPv4 paths that are configured on the VPN devices: 

Control panel:
Network & Sharing Centre 
Network Connections
go into the connection (need to put in admin creds)

Turn off
Microsoft LLDP Protocol Driver
Internet Protocol Version 6 (TCP/IPv6)  
Link-Layer Topology Discovery Responder 
Link-Layer Topology Discovery Mapper I/O Driver

Check the routing table no longer has routes for IPv6 Destinations in it except for at the bottom 

route print 

Check that the default route goes where you want it to and that you can ping or traceroute to a known goog destination such as www.google.com 

Reboot and retest 

guide : 
https://support.zen.co.uk/kb/Knowledgebase/Changing-the-MTU-size-in-Windows-Vista-7-or-8

Settings for Satellite connections  - 
https://www.inmarsat.com/content/dam/inmarsat/corporate/support/fleetbroadband/Inmarsat_TCP_Accelerator_V2.pdf.coredownload.pdf 

Note Cisco VPN client:  Cisco VPN Client normally sets MTU at 1300 so it may be worth going lower that 1420 to 1300. 
https://www.cisco.com/c/en/us/td/docs/security/vpn_client/anyconnect/anyconnect40/administration/guide/b_AnyConnect_Administrator_Guide_4-0/configure-vpn.html 

Cisco Troubleshooting guide:
https://www.cisco.com/c/en/us/td/docs/security/vpn_client/anyconnect/anyconnect40/administration/guide/b_AnyConnect_Administrator_Guide_4-0/troubleshoot-anyconnect.html

Inmarsat info: 
https://www.inmarsat.com/en/support-and-info/support/bgan-firmware.html
go to TCP accellerator version 2 , download Manual & Download program version for windows 7 64 bit. 

64 bit:  https://www.inmarsat.com/content/dam/inmarsat/corporate/support/fleetbroadband/TCP_PEP_Win7_64bit.zip.coredownload.zip
Manual:  https://www.inmarsat.com/content/dam/inmarsat/corporate/support/fleetbroadband/Inmarsat_TCP_Accelerator_V2.pdf.coredownload.pdf 

Any problems please contact me. 

Thanks
Stuart Smiles
@stuart_smiles on twitter.
 
