
Datum 					                1/1


Index
----------

1. Konfiguration Win Server 2008	1
2. Konfiguration Win Client		    2
3. Konfiguration Ubuntu 		      3


Konfiguration Win Server 2008
=============================

NW
----------
NIC2 INTERN:	172.16.33.1/24  Klasse B mit Klasse C Subnetmask
NIC1 Extern:	per DHCP


Server
---------------
Hostname	Server01
Admin-PW	Lap-123


Domaene
---------------
Domaenename	    Domlap.loc
Dom PW		      Passwd
Gesamtstruktur  Server2008R8


DHCP
---------------
Bereichsname:	Bereich1
Bereich:	... - .../24
DNS 		      Server01 (IP)
Router(SGW) 	Server 01(IP)


Daten	
	SW 			Freigabe: Jeder voll oder Auth. User lesen, Dom -Admin Vollz
	Team
	Voelagen
	User
		Profile
	

Konfiguration Client Win7 
=============================



Konfiguration Client  Ubuntu
=============================

