~RPiControl~

~~RaspberryPi 3 Interface~~

~~~Hardware~~~
~~~~Prozessor~~~~
Der RaspberryPi3 ist ein Ein-Platinen-Computer auf der Grundlage der ARM-Prozessorarchitektur, welche durch die Firma Broadcom
lizensiert und im SoC &lt;a href="https://www.raspberrypi.org/wp-
content/uploads/2012/02/BCM2835-ARM-Peripherals.pdf"&gt;BCM2837&lt;/a&gt;
implementiert wurde. Es handelt sich dabei um eine &lt;b&gt;Quad-Core-
SMP&lt;/b&gt;-Architektur mit einem Basistakt von &lt;b&gt;1.2Ghz&lt;/b&gt; und
einer Adressbreite von &lt;b&gt;64-Bit&lt;/b&gt;. 

~~~~GPU~~~~ 
Der BCM2835-Prozessor ist als System-On-Chip konzipiert und stellt einen Grafikprozessor auf
der Grundlage der &lt;a
href="http://elinux.org/Raspberry_Pi_VideoCore_APIs"0&gt;Broadcom-VideoCore
IV&lt;/a&gt; IP bereit. Diese ist in der Lage, Full-HD-Videos abzuspielen und
stellt auch OpenGL ES 2.0 bzw. OpenVG für Anwendungen bereit. ~~~Speicher~~~ Wie
für fast jegliche Art von Computersystem ist auch für den RaspberryPi3 eine
&lt;b&gt;Speicherhierarchie&lt;/b&gt; definiert. Der schnelle, aber flüchtige
Arbeitsspeicher &lt;b&gt;(RAM)&lt;/b&gt; des RaspberryPi ist mit 900Mhz getaktet
(LPDDR2) und steht in einer Kapazität von &lt;b&gt;1GB&lt;/b&gt; bereit. Das
langsame, aber persistente Halten von Daten wird durch eine externe SD-Karte
realisiert. 

~~~~Netzwerk~~~~ 
Ein wesentlicher Unterschied neben der erhöhten
Performance gegenüber dem RaspberryPi2 ist eine neu hinzugekommene Wireless-
Funktionalität. So ist der RPi3 bereits im Auslieferungszustand in der Lage,
&lt;b&gt;Bluetooth-LowEnergy&lt;/b&gt; und WLAN-Verbindungen
(&lt;b&gt;IEEE802.11n&lt;/b&gt;) herzustellen. Diese Funktionalität wird über
den Chipsatz &lt;a
href="http://www.cypress.com/file/298756/download"&gt;BCM43143&lt;/a&gt;
realisiert. Zusätzlich steht wie in den Vorgängermodellen des RPi eine RJ45-
Schnittstelle bereit, über die 100MBit-Ethernetverbindungen hergestellt werden
können. 

~~~~Peripherie~~~~
Zusätzliche Komponenten des RaspberryPi3 sind die
erweiterte Anzahl von USB-Schnittstellen (&lt;b&gt;4x USB 2.0&lt;/b&gt;
gegenüber den 2xUSB1.1 vom ursprünglichen Board aus dem Jahre 2012), welche über
das Bauteil &lt;a
href="http://ww1.microchip.com/downloads/en/DeviceDoc/9514.pdf"&gt;SMSC LAN
9514&lt;/a&gt; realisiert wird (dieses implementiert gleichzeitig auch den
Ethernet-Stack). &lt;p&gt; Daneben ist für den RPi3 auch eine &lt;b&gt;CSI-
Kameraschnittstelle&lt;/b&gt; für serielle Datenübertragung von HD-Kameramodulen
vorgesehen, mit der entsprechende Kameramodule hochauflösend an den BCM-
Prozessor angebunden werden können. &lt;p&gt; Zur Darstellung der
Benutzeroberfläche dient eine &lt;b&gt;HDMI-&lt;/b&gt; und eine &lt;b&gt;DSI-
Displayschnittstelle&lt;/b&gt;, über die mittels Differenzsignalen hochfrequent
und störungsfrei Daten zu Displays übertragen werden können
(&lt;b&gt;LVDS&lt;/b&gt;). Dies entspricht im Wesentlichen dem Verhalten der
HDMI-Schnittstelle, welche zum Anschluss externer Monitore bereitsteht und deren
LVDS-Signale durch die oben genannte VideoCore-GPU generiert werden. &lt;p&gt;
Zur Ausgabe akustischer Signale (Soundkarte) steht ein kombinierter A/V-Adapter
zur Verfügung, der durch eine 3.5mm Klinkenstecker eine Stereoausgabe
ermöglicht. Zusätzlich wird über einen dritten Kanal ein Composite-Videosignal
(PAL/NTSC) bereitgestellt, was zur Videoausgabe auf nicht-HDMI-kompatibler
Hardware verwendet werden kann. ~~~Erweiterungen~~~ Für das hier dokumentierte
Projekt ist allerdings eine andere Eigenschaft des RaspberryPi entscheidend: der
RaspberryPi 3 besitzt nämlich eine 40-polige Steckerleiste zur Anbindung
externer Peripherie. Darüber können universell benutzbare Ein-/Ausgabe-Pins
(&lt;b&gt;GPIO=General Purpose I/O&lt;/b&gt;) mit LVTTL Pegeln
(&lt;b&gt;3.3V&lt;/b&gt;) geschaltet bzw. hochohmig gelesen werden. Manche
dieser GPIO Pins besitzen eine Doppelbelegung, die bei Konfiguration der
richtigen Register des BroadCom-SoCs die Zweitfunktionalität freischaltet. Dies
betrifft z.B. Platinenbusse wie &lt;b&gt;SPI&lt;/b&gt; oder
&lt;b&gt;I²C&lt;/b&gt;, die Ansteuerung von RS232-/ oder RS485-Treibern
(&lt;b&gt;UART&lt;/b&gt;), aber auch die Generierung von externen Signalformen
mittels Hardware-unterstützter Pulsweitenmodulation (&lt;b&gt;PWM&lt;/b&gt;).
Maximal belastbar sind die GPIO-Ausgabekanäle mit &lt;b&gt;50mA&lt;/b&gt;, was
zum direkten Schalten von LEDs ausreicht, für größere Lasten aber Bipolar- bzw.
Feldeffekttransistoren benötigt.

~~~Betriebssystem~~~ 
Der RaspberryPi kann mit verschiedenen Betriebssystemen
betrieben werden. Unter anderem stehen verschiedene Linux-Distributionen wie
&lt;a href="Raspbian"&gt;Raspbian&lt;/a&gt; oder das für MediaCenter optimierte
&lt;a href="http://www.openelec.tv"&gt;OpenELEC&lt;/a&gt; zur Verfügung. Auch
eine Verwendung mit Microsoft-Plattformen ist möglich, so kann etwa auch &lt;a
href="https://developer.microsoft.com/de-de/windows/iot"&gt;Windows10-
IoT&lt;/a&gt; für den RaspberryPi3 verwendet werden.

~~~~Programmierung~~~~

Zur Programmierung eigener Anwendungen ist für Linux-
Betriebssysteme die Programmiersprache &lt;a
href="http://www.python.org"&gt;Python&lt;/a&gt; das Mittel der Wahl. Sie stellt
eine sehr einfache und für Einsteiger leicht zu erlernende Syntax bereit und
kann durch &lt;a
href="https://riverbankcomputing.com/software/pyqt/intro"&gt;PyQT&lt;/a&gt;
leicht grafische Anwendungen erzeugen. Zur Ansteuerung der GPIOs kann die
Softwarekomponente &lt;a href="http://raspberrypiguide.de/howtos/raspberry-pi-
gpio-how-to/"&gt;WiringPi&lt;/a&gt; genutzt werden. Neben Python stehen auch
Compiler für Programmiersprachen wie C/C++, Java oder &lt;a
href="http://www.adacore.com/press/adacore-introduces-gnat-gpl-2015-for-the-
raspberry-pi-2/"&gt;ADA&lt;/a&gt; bereit. &lt;p&gt; Für die Verwendung von
Windows 10 IoT muss statt dessen das &lt;a
href="https://developer.microsoft.com/en-
us/windows/iot/docs/setuppcrpi"&gt;VisualStudio 2015&lt;/a&gt; verwendet werden.
Damit wird eine Programmierung mit C# und dem .NET Framework
möglich.


~~GPIO-Extender~~

Hauptkomponente des Projekts ist der integrierte Schaltkreis
&lt;a href="http://cdn-
reichelt.de/documents/datenblatt/A200/DS_MCP23017.pdf"&gt;MCP23017&lt;/a&gt;,
der als GPIO-Extender fungiert und über den I²C-Bus vom RaspberryPi aus
gesteuert werden kann. &lt;p&gt; Die wesentliche Aufgabe des Bausteins ist die
Behebung der Limitierung von I/O-Ports. Der RaspberryPi kann als I²C-Master
theoretisch bis zu 127 Slaves adressieren, die Einschränkung soll hier bei
maximal 8 Teilnehmern liegen.&lt;p&gt; Der MCP23017 unterstützt zwei Kanäle mit
je einer Breite von 8-Bit. Durch Konfiguration eines Datenrichtungsregisters
können deren Pins zwischen Input- und Output umgeschaltet werden.


~~Expansion-Header~~ 
Die Expansion-Header entsprechen Stiftleisten
zur Erweiterung der Funktionalität. So können für ein bestimmte Einsatzzweck
erstellte Lochraster- bzw. Platinenaufbauten mit dem Board verwendet werden,
solange sie den gleichen Footprint verwenden und die elektrischen Gegebenheiten
passend antizipieren.</description>


~~RJ-45-Steckverbinder~~
Zur Verbindung von Busteilnehmern kommen RJ-
45-Steckverbinder zum Einsatz, die in der Netzwerktechnik weit verbreitet sind
und daher leicht verfügbar bzw. erweiterbar sind. Das betrifft hauptsächlich die
einfache und wartungsfreie Montage von Slave-Modulen im Gesamtsystem des
Messeaufbaus.&lt;p&gt; &lt;b&gt;Keine Kompatibilität zu Ethernet-Switches/-
Hubs!&lt;/b&gt; &lt;p&gt; Die Belegung  der RJ-45-Buchse ist &lt;b&gt;proprietär
und inkompatibel zu Ethernet&lt;/b&gt;. 

Konkret leisten muss die RJ45-Buchse:
• Masseverbindung
• Reserviert
• I²C-Clock (+3.3V LVTTL)
• I²C-Data (+3.3V LVTTL)
• +12V DC-Versorgungsspannung
• Reset (Low-Active, +3.3V LVTTL)
• Reserviert
• Reserviert

Somit wird sichergestellt, dass selbst bei Verklemmung des I²C-Busses, ein durch
den I²C-Master gesteuertes Reset ausgelöst werden kann. Die restlichen Aufgaben
sind Datentransport und Bereitstellung einer gemeinsamen Spannungsquelle für
alle Slaves. &lt;p&gt; Die handelsüblichen Cat5-Kabel bieten für dieses kleine
I²C-Bussystem auch den Vorteil einer recht hohen Abschirmung gegenüber HF-
Einströmungen, da die Adern paarweise geschirmt sind (Twisted-Pair). Damit
sollte eine für PWM ausreichend hohe Taktung des I²C-Busses auch über mal 2-3m
hin gewährleistet sein.</description> <plain>


~~I²C-Bus~~
Zur Kommunikation zwischen RaspberryPi und den
angeschlossenen Verbrauchern dient der Philips entwickelte I²C-Bus, der ähnlich
wie der SPI-Bus zur Kommunikation zwischen IC auf und zwischen Leiterplatten
dient (&lt;strong&gt;I²C=Inter-Integrated-Circuits&lt;/strong&gt;). Aus diesem
Design folgen ein paar ernsthafte Limitierungen:&lt;ul&gt; •  Der I²C-Bus ist
&lt;strong&gt;nicht differentiell&lt;/strong&gt;, d.h. es wird
&lt;strong&gt;nicht&lt;/strong&gt; wie etwa bei CAN- oder RS485 mit zwei
Datenpotentialen (D+, D-) gearbeitet, deren Differenzspannung vom Empfänger
gebildet wird.&lt;/li&gt; • I²C ist somit anfällig für Gleichtaktstörungen (z.B.
Zündfunken), hat aufgrund der niedrigen (LV)TTL-Pegel eine begrenzte Reichweite
und benötigt ähnlich wie die RS232 immer eine gemeinsame Masse als
Bezugspotential.&lt;/li&gt; • I²C ist ein &lt;strong&gt;getakteter
Bus&lt;/strong&gt;&lt;/li&gt; • I²C ist ein &lt;strong&gt;Master-Slave-
Bussystem&lt;/strong&gt;&lt;/li&gt; • Anzahl Teilnehmer ist auf 127
begrenzt&lt;/li&gt; • Datenbreite für Register ist im Durchschnitt bei 16-Bit
(implementierungabhängig)&lt;/li&gt; • Terminierung erforderlich&lt;/li&gt; •
Datenraten von bis zu 5Mbit/s möglich&lt;/li&gt; • serieller Bus (MSB-first
Übertragung)&lt;/li&gt; &lt;/ul&gt; &lt;p&gt; Diese Master-Slave-Busarchitektur
ermöglicht es dem Master, zyklisch Werte vom Bus abzufragen
(&lt;strong&gt;Polling&lt;/strong&gt;). Manche IC-Implementierungen ermöglichen
zusätzlich die Verwendung von externen Interrupt-Pins, welche OnChange-
Ereignisse signalisieren können. Aufgrund der dadurch resultierenden
Verdrahtungskomplexität bietet sich das allerdings nur in speziellen
Anwendungsfällen an, wo z.B. ein preiswerter und leistungsbegrenzter 8-Bit-
Mikrocontroller (möglicherweise mit Optimierung auf maximale Batterielaufzeit)
aufgrund eigener Resourcenrestriktionen und anderen integrierten Funktionen
nicht ständig auf den I²C-Bus pollen kann.&lt;p&gt; Aus der Perspektive des
RaspberryPi als I²C-Master bietet sich I²C sehr an, da mit den &lt;b&gt;i2c-
tools&lt;/b&gt; und den Linux-Kernel-Modul &lt;b&gt;i2c-bcm2708&lt;/b&gt; eine
sehr leistungsstarke und komfortable Schnittstelle zur Arbeit mit I²C bereit
steht. Die sehr gute Linux-Unterstützung für I²C rührt u.a. historisch auch
daher, dass viele Temperatur-Sensoren auf PC-Mainboards über dieses Protokoll
adressiert wurden (Stichwort &lt;b&gt;lm-sensors&lt;/b&gt;). &lt;p&gt; Die I²C-
Slaves als Teilnehmer müssen mit &lt;b&gt;eindeutigen Adressen&lt;/b&gt; kodiert
sein. Zu diesem Zweck dienen beim MCP23017 die Pins A[0..2], wodurch sich 2³=8
Teilnehmer unterscheiden lassen. Die Slave-Adressierung wird durch den
montierten DIP-Schalter durchgeführt.


~~Versorgung~~
Die Spannungsversorgung ist einheitlich auf +12V DC sichergestellt. Dies zum Einen dem Leistungsteil geschuldet, dessen Verbraucher
diese Spannung erfordern, zum Anderen bietet sich dieser Spannungslevel aufgrund
der Versorgung durch Kfz-Netzteile etc. an. &lt;p&gt; Eine wichtige Rolle für
die Versorgungsspannung spielt der I²C-Bus, der zur Kommunikation zwischen dem
RaspberryPi und den Busteilnehmern dient. I²C funktioniert im Gegensatz zu CAN-
Bus oder anderen Feldbussystemen wie RS-485 &lt;strong&gt;nicht
differenziell&lt;/strong&gt;. Das bedeutet in der Konsequenz, dass sowohl
&lt;strong&gt;eine gemeinsame Masse&lt;/strong&gt;, als auch &lt;strong&gt;ein
gemeinsames Bezugspotential&lt;/strong&gt; notwendig ist.&lt;p&gt; Der Broadcom-
ARM-Prozessor des RaspberryPi verwendet sowohl für GPIOs, als auch für SPI und
I²C-Bus ein LVTTL-Pegel, d.h. +3.3V, welche sowohl für den I²C-Takt, als auch
für die I²C-Datenleitung gelten.&lt;p&gt; Somit ergibt sich in der Konsequenz,
dass als kleinster gemeinsamer Nenner zwischen RaspberryPi und GPIO-Extender
beide auf LVTTL betrieben werden sollten. &lt;p&gt; Für diese Zwecke wird ein
Low-Drop-Spannungsregler von Texas Instruments vom Typ &lt;a
href="http://www.ti.com/lit/ds/symlink/lm1117.pdf"&gt;LM1117&lt;/a&gt;
eingesetzt.