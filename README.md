# WIN.SRV
## Windows Server Stuff

You live Linux butt (sic!) sometimes meet a window ...

### Windows: Server 2008R2 + Client Windows7 + Client Ubuntu

- Server 2008 R2 as Domain Controller for
- Client Windows 7
- Client Ubuntu

#### NOTES

Active Directory Administrative Center (ADAC)  
- http://windowsitpro.com/windows-server-2008/using-active-directory-administrative-center-windows-server-2008-r2

Installed by default w/ Active Directory Domain Services (AD DS) role.  
Included in Remote Server Administration Tools (RSAT) feature.

Netzwerkrichtlinien- und Zugriffsdienste  
- http://openbook.rheinwerk-verlag.de/windows_server_2008/windows_server_2008_kap_14_001.htm#mj69794be7e4b121d858f62a9f3245e13a
- https://technet.microsoft.com/en-us/library/cc754516(v=ws.10).aspx		# Netsh Command Reference


Servermanager
------------------

Hostname:

	netdom -renamecomputer $env:computername -newname:Server01
	j 					# NICHT ja
	Restart-Computer


NICs:

	Nachm dcpromo.exe vorm DHCP u DNS nochmal statt 127... die 172.16.33.1 eingeben.


DCPromo:

	Neue Domaene in GesamtStruktur (DomaenenForrest)
	DOMLAP.local
	"Ja" bei "Unterschiedl. IPs"
	Protokoll, Sysvol, ... auf Standard gelassen
	Passwd: 123-# ?????????????????????????? Pa$$w0rd
	Auto-Neustart

Jetzt bei Extern DNS auf 172.16.33.1

Role, Feature

	https://duckduckgo.com/?q=add-windowsfeature+role&t=ffab&ia=web
	>
	https://technet.microsoft.com/en-us/library/cc754923(v=ws.11).aspx .................... # Role vs Feature  
	https://technet.microsoft.com/en-us/library/hh831809(v=ws.11).aspx#BKMK_installwps .... # Syntax  
	https://www.petri.com/windows-features-with-powershell-part-2 ......................... # Beispiel-Script  
	https://technet.microsoft.com/en-us/library/cc794771(v=ws.10).aspx .................... # Administering DNS Server  
	https://technet.microsoft.com/en-us/library/hh831809(v=ws.11).aspx#BKMK_batch ......... # Install Roles  
	https://technet.microsoft.com/de-de/windowsserver/bb310558.aspx ....................... # !!!!!!!!!!! all Roles unten  
	https://technet.microsoft.com/en-us/library/68ce4f7c-b8e2-4b1a-9909-9674f1738e7c ...... # Network Policy, Access Services  
	https://technet.microsoft.com/en-us/library/cc754634 .................................. # R & RAS  
	DHCP, NW-Richtlinie 

Lease:

	8 Tage  
	statusfrei  
	akt  

DHCP:

	MAC aus VirtualBox Client-Einstellungen Ubuntu (nicht im Linux)
	
Role install:

	dism /enable-feature /featurename:DHCPServer /online
	
Change Service:  

	sc config DHCPServer start= auto		# Eric Tierling: 389
	
Start NOW for configuration:  

	net start DHCPServer

GPO:  

	Verwaltung  
	Bei Ueberpruefen der Serveroptionen gleich Router-Name Server01 rein

DNS:
	Test
	```
	ipconfig -all
	```
	Nur 116.16.33 - kein alternativer DNS

Bed. Weiterl.

	Dienste > DNS-Dom> BFI 10.10.10.8 >> Dann gibt er FQDN selbst an.
	(Google 8.8.8.8 ginge auch...)

RAS:  

	Verwaltung
	NAT
	Fast nix einstellen

USER, ORDNER:

	neu C:\Daten und rekursiv und auch Backup

	C
	 |_Daten	
	 | | Users
	 | | |_Profile: G.jeder:     voll
	 | |_Software:  G.admins:    voll
	 | |            G.auth.user: voll 
	 | |_Team
	 | |_Verwaltung: 
	 |_Backup
   

Gleich Shares:  

	erweiterte, Profile: jeder voll (jeder soll selbst)  
	User: 		Profilpfad \\  
	SW: 		- entfernen Auth  
			- Admins rein mit Voll (damit ich vom Netz aus was aendern kann)  
	Team: 		Achtung, bitte warten, erst:  
	Verwaltung: 	Neue OU Office + Kunden  
	Neue Gruppe: 	Verwaltung. 1. Haken raus, 2. + 3. rein. Keep. Global User lauft nicht ab und (kann sich einloggen?)  
	Kunden 3: 	Nein,  2 ja,  3 ja,  4 nein.  
	Team:		Kein Voll, aber aendern + lesen.  
	Vorlagen: 	Admins haben Minus. Domaenennutzer: Aendern + lesen.  
	Backup: 	Jeder raus; ansonsten Voll  

FTP jetzt  
	Sicherheit: Vertrauensw. XXX ftp://...2008
	User0x > PW: P...x#
