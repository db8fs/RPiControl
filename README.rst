
##########
RPiControl
##########

***************************
RaspberryPi 3 Interface
***************************

Hardware
==============

Prozessor
^^^^^^^^^

Der RaspberryPi3 ist ein Ein-Platinen-Computer auf der Grundlage der ARM-Prozessorarchitektur, welche durch die Firma Broadcom lizensiert und im SoC (https://www.raspberrypi.org/wp-content/uploads/2012/02/BCM2835-ARM-Peripherals.pdf) implementiert wurde. Es handelt sich dabei um eine **Quad-Core-SMP**-Architektur mit einem Basistakt von **1.2Ghz** und einer Adressbreite von **64-Bit**. 

GPU
^^^
Der BCM2835-Prozessor ist als System-On-Chip konzipiert und stellt einen Grafikprozessor auf der Grundlage der Broadcom-VideoCoreIV-IP (http://elinux.org/Raspberry_Pi_VideoCore_APIs) bereit. Diese ist in der Lage, Full-HD-Videos abzuspielen und stellt auch OpenGL ES 2.0 bzw. OpenVG für Anwendungen bereit.

Speicher
^^^^^^^^
Wie für fast jegliche Art von Computersystem ist auch für den RaspberryPi3 eine **Speicherhierarchie** definiert. Der schnelle, aber flüchtige Arbeitsspeicher (**RAM**) des RaspberryPi ist mit 900Mhz getaktet (LPDDR2) und steht in einer Kapazität von **1GB** bereit. Das langsame, aber persistente Halten von Daten wird durch eine externe SD-Karte realisiert. 

Netzwerk
^^^^^^^^

Ein wesentlicher Unterschied neben der erhöhten Performance gegenüber dem RaspberryPi2 ist eine neu hinzugekommene Wireless-Funktionalität. So ist der RPi3 bereits im Auslieferungszustand in der Lage, **Bluetooth-LowEnergy** und WLAN-Verbindungen (IEEE 802.11n) herzustellen. Diese Funktionalität wird über den Chipsatz BCM43143 (http://www.cypress.com/file/298756/download) realisiert. Zusätzlich steht wie in den Vorgängermodellen des RPi eine RJ45-Schnittstelle bereit, über die 100MBit-Ethernetverbindungen hergestellt werden können. 

Peripherie
^^^^^^^^^^

Zusätzliche Komponenten des RaspberryPi3 sind die erweiterte Anzahl von USB-Schnittstellen (4x USB 2.0) gegenüber den 2xUSB1.1 vom ursprünglichen Board aus dem Jahre 2012), welche über das Bauteil SMSC LAN9514 (http://ww1.microchip.com/downloads/en/DeviceDoc/9514.pdf) realisiert wird (dieses implementiert gleichzeitig auch den Ethernet-Stack). 
Daneben ist für den RPi3 auch eine **CSI-Kameraschnittstelle** für serielle Datenübertragung von HD-Kameramodulen vorgesehen, mit der entsprechende Kameramodule hochauflösend an den BCM-Prozessor angebunden werden können. 

Zur Darstellung der Benutzeroberfläche dient eine **HDMI-** und eine **DSI-Displayschnittstelle**, über die mittels Differenzsignalen hochfrequent und störungsfrei Daten zu Displays übertragen werden können (**LVDS**). Dies entspricht im Wesentlichen dem Verhalten der HDMI-Schnittstelle, welche zum Anschluss externer Monitore bereitsteht und deren LVDS-Signale durch die oben genannte VideoCore-GPU generiert werden. 

Zur Ausgabe akustischer Signale (Soundkarte) steht ein kombinierter A/V-Adapter zur Verfügung, der durch eine 3.5mm Klinkenstecker eine Stereoausgabe ermöglicht. Zusätzlich wird über einen dritten Kanal ein Composite-Videosignal (PAL/NTSC) bereitgestellt, was zur Videoausgabe auf nicht-HDMI-kompatibler Hardware verwendet werden kann. 

Erweiterungen
^^^^^^^^^^^^^
Für das hier dokumentierte Projekt ist allerdings eine andere Eigenschaft des RaspberryPi entscheidend: der RaspberryPi 3 besitzt nämlich eine 40-polige Steckerleiste zur Anbindung
externer Peripherie. Darüber können universell benutzbare Ein-/Ausgabe-Pins (GPIO=General Purpose I/O) mit LVTTL Pegeln (**3.3V**) geschaltet bzw. hochohmig gelesen werden. Manche
dieser GPIO Pins besitzen eine Doppelbelegung, die bei Konfiguration der richtigen Register des BroadCom-SoCs die Zweitfunktionalität freischaltet. Dies betrifft z.B. Platinenbusse wie **SPI** oder **I²C**, die Ansteuerung von RS232-/ oder RS485-Treibern (**UART**), aber auch die Generierung von externen Signalformen mittels Hardware-unterstützter Pulsweitenmodulation (**PWM**).
Maximal belastbar sind die GPIO-Ausgabekanäle mit **50mA**, was zum direkten Schalten von LEDs ausreicht, für größere Lasten aber Bipolar- bzw. Feldeffekttransistoren benötigt.

Betriebssystem
^^^^^^^^^^^^^^

Der RaspberryPi kann mit verschiedenen Betriebssystemen betrieben werden. Unter anderem stehen verschiedene Linux-Distributionen wie Raspbian (http://www.raspbian.org) oder das für MediaCenter optimierte (http://www.openelec.tv) zur Verfügung. Auch eine Verwendung mit Microsoft-Plattformen ist möglich, so kann etwa auch Windows10-IoT (https://developer.microsoft.com/de-de/windows/iot) für den RaspberryPi3 verwendet werden.

Programmierung
^^^^^^^^^^^^^^

Zur Programmierung eigener Anwendungen ist für Linux-Betriebssysteme die Programmiersprache **Python** (http://www.python.org) das Mittel der Wahl. Sie stellt eine sehr einfache und für Einsteiger leicht zu erlernende Syntax bereit und kann durch **PyQt** (https://riverbankcomputing.com/software/pyqt/intro) leicht grafische Anwendungen erzeugen. Zur Ansteuerung der GPIOs kann die Softwarekomponente **WiringPi** (http://raspberrypiguide.de/howtos/raspberry-pi-gpio-how-to/) genutzt werden. Neben Python stehen auch Compiler für Programmiersprachen wie C/C++, Java oder ADA (http://www.adacore.com/press/adacore-introduces-gnat-gpl-2015-for-the-raspberry-pi-2) bereit. 

Für die Verwendung von Windows 10 IoT muss statt dessen das VisualStudio 2015 (https://developer.microsoft.com/en-us/windows/iot/docs/setuppcrpi) verwendet werden. Damit wird eine Programmierung mit **C#** und dem **.NET Framework** möglich.


GPIO-Extender
^^^^^^^^^^^^^

Hauptkomponente des Projekts ist der integrierte Schaltkreis MCP23017 (http://cdn-reichelt.de/documents/datenblatt/A200/DS_MCP23017.pdf), der als GPIO-Extender fungiert und über den I²C-Bus vom RaspberryPi aus gesteuert werden kann.

Die wesentliche Aufgabe des Bausteins ist die Behebung der Limitierung von I/O-Ports. Der RaspberryPi kann als I²C-Master theoretisch bis zu 127 Slaves adressieren, die Einschränkung soll hier bei maximal 8 Teilnehmern liegen.&lt;p&gt; Der MCP23017 unterstützt zwei Kanäle mit je einer Breite von 8-Bit. Durch Konfiguration eines Datenrichtungsregisters können deren Pins zwischen Input- und Output umgeschaltet werden.


Expansion-Header
^^^^^^^^^^^^^^^^
Die Expansion-Header entsprechen Stiftleisten zur Erweiterung der Funktionalität. So können für ein bestimmte Einsatzzweck erstellte Lochraster- bzw. Platinenaufbauten mit dem Board verwendet werden, solange sie den gleichen Footprint verwenden und die elektrischen Gegebenheiten passend antizipieren.


RJ-45-Steckverbinder
^^^^^^^^^^^^^^^^^^^^^
Zur Verbindung von Busteilnehmern kommen RJ-45-Steckverbinder zum Einsatz, die in der Netzwerktechnik weit verbreitet sind und daher leicht verfügbar bzw. erweiterbar sind. Das betrifft hauptsächlich die einfache und wartungsfreie Montage von Slave-Modulen im Gesamtsystem des Aufbaus. 

**Keine Kompatibilität zu Ethernet-Switches/-Hubs**!

Die Belegung  der RJ-45-Buchse ist **proprietär und inkompatibel zu Ethernet**. 

Konkret leisten muss die RJ45-Buchse:

- Masseverbindung
- Reserviert
- I²C-Clock (+3.3V LVTTL)
- I²C-Data (+3.3V LVTTL)
- +12V DC-Versorgungsspannung
- Reset (Low-Active, +3.3V LVTTL)
- Reserviert
- Reserviert

Somit wird sichergestellt, dass selbst bei Verklemmung des I²C-Busses, ein durch den I²C-Master gesteuertes Reset ausgelöst werden kann. Die restlichen Aufgaben sind Datentransport und Bereitstellung einer gemeinsamen Spannungsquelle für alle Slaves. Die handelsüblichen Cat5-Kabel bieten für dieses kleine I²C-Bussystem auch den Vorteil einer recht hohen Abschirmung gegenüber HF-Einströmungen, da die Adern paarweise geschirmt sind (Twisted-Pair). Damit sollte eine für PWM ausreichend hohe Taktung des I²C-Busses auch über mal 2-3m
hin gewährleistet sein.


I²C-Bus
^^^^^^^
Zur Kommunikation zwischen RaspberryPi und den angeschlossenen Verbrauchern dient der von Philips entwickelte I²C-Bus, der ähnlich wie der SPI-Bus zur Kommunikation zwischen IC auf und zwischen Leiterplatten dient (**I²C=Inter-Integrated-Circuits**). Aus diesem Design folgen ein paar ernsthafte Limitierungen:

- Der I²C-Bus ist **nicht differentiell**, d.h. es wird **nicht** wie etwa bei CAN- oder RS485 mit zwei Datenpotentialen (D+, D-) gearbeitet, deren Differenzspannung vom Empfänger gebildet wird.
- I²C ist somit anfällig für Gleichtaktstörungen (z.B. Zündfunken), hat aufgrund der niedrigen (LV)TTL-Pegel eine begrenzte Reichweite und benötigt ähnlich wie die RS232 immer eine gemeinsame Masse als Bezugspotential.
- I²C ist ein **getakteter Bus**
- I²C ist ein Master-Slave-Bussystem 
- Anzahl Teilnehmer ist auf 127 begrenzt
- Datenbreite für Register ist im Durchschnitt bei 16-Bit (implementierungabhängig)
- Terminierung erforderlich
- Datenraten von bis zu 5Mbit/s möglich
- serieller Bus (MSB-first Übertragung)

Diese Master-Slave-Busarchitektur ermöglicht es dem Master, zyklisch Werte vom Bus abzufragen
(**Polling**). Manche IC-Implementierungen ermöglichen zusätzlich die Verwendung von externen Interrupt-Pins, welche OnChange-Ereignisse signalisieren können. Aufgrund der dadurch resultierenden Verdrahtungskomplexität bietet sich das allerdings nur in speziellen Anwendungsfällen an, wo z.B. ein preiswerter und leistungsbegrenzter 8-Bit-Mikrocontroller (möglicherweise mit Optimierung auf maximale Batterielaufzeit) aufgrund eigener Resourcenrestriktionen und anderen integrierten Funktionen nicht ständig auf den I²C-Bus pollen kann.

Aus der Perspektive des RaspberryPi als I²C-Master bietet sich I²C sehr an, da mit den **i2c-tools** und dem Linux-Kernel-Modul **i2c-bcm2708** eine sehr leistungsstarke und komfortable Schnittstelle zur Arbeit mit I²C bereit steht. Die sehr gute Linux-Unterstützung für I²C rührt u.a. historisch auch daher, dass viele Temperatur-Sensoren auf PC-Mainboards über dieses Protokoll adressiert wurden (Stichwort **lm-sensors**).

Die I²C-Slaves als Teilnehmer müssen mit **eindeutigen Adressen** kodiert sein. Zu diesem Zweck dienen beim MCP23017 die Pins A[0..2], wodurch sich 2³=8 Teilnehmer unterscheiden lassen. Die Slave-Adressierung wird durch den montierten DIP-Schalter durchgeführt.


Versorgung
^^^^^^^^^^
Die Spannungsversorgung ist einheitlich auf +12V DC sichergestellt. Dies zum Einen dem Leistungsteil geschuldet, dessen Verbraucher diese Spannung erfordern, zum Anderen bietet sich dieser Spannungslevel aufgrund der Versorgung durch Kfz-Netzteile etc. an. 
Eine wichtige Rolle für die Versorgungsspannung spielt der I²C-Bus, der zur Kommunikation zwischen dem RaspberryPi und den Busteilnehmern dient. I²C funktioniert im Gegensatz zu CAN-
Bus oder anderen Feldbussystemen wie RS-485 **nicht differenziell**. Das bedeutet in der Konsequenz, dass sowohl **eine gemeinsame Masse**, als auch **ein gemeinsames Versorgungpotential** notwendig ist.

Der Broadcom-ARM-Prozessor des RaspberryPi verwendet sowohl für GPIOs, als auch für SPI und I²C-Bus ein LVTTL-Pegel, d.h. +3.3V, welche sowohl für den I²C-Takt, als auch
für die I²C-Datenleitung gelten.

Somit ergibt sich in der Konsequenz, dass als kleinster gemeinsamer Nenner zwischen RaspberryPi und GPIO-Extender beide auf LVTTL betrieben werden sollten.

Für diese Zwecke wird ein Low-Drop-Spannungsregler von Texas Instruments vom Typ **LM1117** (http://www.ti.com/lit/ds/symlink/lm1117.pdf) eingesetzt.