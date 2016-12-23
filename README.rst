
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
Der BCM2835-Prozessor ist als System-On-Chip konzipiert und stellt einen Grafikprozessor auf der Grundlage der Broadcom-VideoCoreIV-IP (http://elinux.org/Raspberry_Pi_VideoCore_APIs) bereit. Diese ist in der Lage, Full-HD-Videos abzuspielen und stellt auch OpenGL ES 2.0 bzw. OpenVG f�r Anwendungen bereit.

Speicher
^^^^^^^^
Wie f�r fast jegliche Art von Computersystem ist auch f�r den RaspberryPi3 eine **Speicherhierarchie** definiert. Der schnelle, aber fl�chtige Arbeitsspeicher (**RAM**) des RaspberryPi ist mit 900Mhz getaktet (LPDDR2) und steht in einer Kapazit�t von **1GB** bereit. Das langsame, aber persistente Halten von Daten wird durch eine externe SD-Karte realisiert. 

Netzwerk
^^^^^^^^

Ein wesentlicher Unterschied neben der erh�hten Performance gegen�ber dem RaspberryPi2 ist eine neu hinzugekommene Wireless-Funktionalit�t. So ist der RPi3 bereits im Auslieferungszustand in der Lage, **Bluetooth-LowEnergy** und WLAN-Verbindungen (IEEE 802.11n) herzustellen. Diese Funktionalit�t wird �ber den Chipsatz BCM43143 (http://www.cypress.com/file/298756/download) realisiert. Zus�tzlich steht wie in den Vorg�ngermodellen des RPi eine RJ45-Schnittstelle bereit, �ber die 100MBit-Ethernetverbindungen hergestellt werden k�nnen. 

Peripherie
^^^^^^^^^^

Zus�tzliche Komponenten des RaspberryPi3 sind die erweiterte Anzahl von USB-Schnittstellen (4x USB 2.0) gegen�ber den 2xUSB1.1 vom urspr�nglichen Board aus dem Jahre 2012), welche �ber das Bauteil SMSC LAN9514 (http://ww1.microchip.com/downloads/en/DeviceDoc/9514.pdf) realisiert wird (dieses implementiert gleichzeitig auch den Ethernet-Stack). 
Daneben ist f�r den RPi3 auch eine **CSI-Kameraschnittstelle** f�r serielle Daten�bertragung von HD-Kameramodulen vorgesehen, mit der entsprechende Kameramodule hochaufl�send an den BCM-Prozessor angebunden werden k�nnen. 

Zur Darstellung der Benutzeroberfl�che dient eine **HDMI-** und eine **DSI-Displayschnittstelle**, �ber die mittels Differenzsignalen hochfrequent und st�rungsfrei Daten zu Displays �bertragen werden k�nnen (**LVDS**). Dies entspricht im Wesentlichen dem Verhalten der HDMI-Schnittstelle, welche zum Anschluss externer Monitore bereitsteht und deren LVDS-Signale durch die oben genannte VideoCore-GPU generiert werden. 

Zur Ausgabe akustischer Signale (Soundkarte) steht ein kombinierter A/V-Adapter zur Verf�gung, der durch eine 3.5mm Klinkenstecker eine Stereoausgabe erm�glicht. Zus�tzlich wird �ber einen dritten Kanal ein Composite-Videosignal (PAL/NTSC) bereitgestellt, was zur Videoausgabe auf nicht-HDMI-kompatibler Hardware verwendet werden kann. 

Erweiterungen
^^^^^^^^^^^^^
F�r das hier dokumentierte Projekt ist allerdings eine andere Eigenschaft des RaspberryPi entscheidend: der RaspberryPi 3 besitzt n�mlich eine 40-polige Steckerleiste zur Anbindung
externer Peripherie. Dar�ber k�nnen universell benutzbare Ein-/Ausgabe-Pins (GPIO=General Purpose I/O) mit LVTTL Pegeln (**3.3V**) geschaltet bzw. hochohmig gelesen werden. Manche
dieser GPIO Pins besitzen eine Doppelbelegung, die bei Konfiguration der richtigen Register des BroadCom-SoCs die Zweitfunktionalit�t freischaltet. Dies betrifft z.B. Platinenbusse wie **SPI** oder **I�C**, die Ansteuerung von RS232-/ oder RS485-Treibern (**UART**), aber auch die Generierung von externen Signalformen mittels Hardware-unterst�tzter Pulsweitenmodulation (**PWM**).
Maximal belastbar sind die GPIO-Ausgabekan�le mit **50mA**, was zum direkten Schalten von LEDs ausreicht, f�r gr��ere Lasten aber Bipolar- bzw. Feldeffekttransistoren ben�tigt.

Betriebssystem
^^^^^^^^^^^^^^

Der RaspberryPi kann mit verschiedenen Betriebssystemen betrieben werden. Unter anderem stehen verschiedene Linux-Distributionen wie Raspbian (http://www.raspbian.org) oder das f�r MediaCenter optimierte (http://www.openelec.tv) zur Verf�gung. Auch eine Verwendung mit Microsoft-Plattformen ist m�glich, so kann etwa auch Windows10-IoT (https://developer.microsoft.com/de-de/windows/iot) f�r den RaspberryPi3 verwendet werden.

Programmierung
^^^^^^^^^^^^^^

Zur Programmierung eigener Anwendungen ist f�r Linux-Betriebssysteme die Programmiersprache **Python** (http://www.python.org) das Mittel der Wahl. Sie stellt eine sehr einfache und f�r Einsteiger leicht zu erlernende Syntax bereit und kann durch **PyQt** (https://riverbankcomputing.com/software/pyqt/intro) leicht grafische Anwendungen erzeugen. Zur Ansteuerung der GPIOs kann die Softwarekomponente **WiringPi** (http://raspberrypiguide.de/howtos/raspberry-pi-gpio-how-to/) genutzt werden. Neben Python stehen auch Compiler f�r Programmiersprachen wie C/C++, Java oder ADA (http://www.adacore.com/press/adacore-introduces-gnat-gpl-2015-for-the-raspberry-pi-2) bereit. 

F�r die Verwendung von Windows 10 IoT muss statt dessen das VisualStudio 2015 (https://developer.microsoft.com/en-us/windows/iot/docs/setuppcrpi) verwendet werden. Damit wird eine Programmierung mit **C#** und dem **.NET Framework** m�glich.


GPIO-Extender
^^^^^^^^^^^^^

Hauptkomponente des Projekts ist der integrierte Schaltkreis MCP23017 (http://cdn-reichelt.de/documents/datenblatt/A200/DS_MCP23017.pdf), der als GPIO-Extender fungiert und �ber den I�C-Bus vom RaspberryPi aus gesteuert werden kann.

Die wesentliche Aufgabe des Bausteins ist die Behebung der Limitierung von I/O-Ports. Der RaspberryPi kann als I�C-Master theoretisch bis zu 127 Slaves adressieren, die Einschr�nkung soll hier bei maximal 8 Teilnehmern liegen.&lt;p&gt; Der MCP23017 unterst�tzt zwei Kan�le mit je einer Breite von 8-Bit. Durch Konfiguration eines Datenrichtungsregisters k�nnen deren Pins zwischen Input- und Output umgeschaltet werden.


Expansion-Header
^^^^^^^^^^^^^^^^
Die Expansion-Header entsprechen Stiftleisten zur Erweiterung der Funktionalit�t. So k�nnen f�r ein bestimmte Einsatzzweck erstellte Lochraster- bzw. Platinenaufbauten mit dem Board verwendet werden, solange sie den gleichen Footprint verwenden und die elektrischen Gegebenheiten passend antizipieren.


RJ-45-Steckverbinder
^^^^^^^^^^^^^^^^^^^^^
Zur Verbindung von Busteilnehmern kommen RJ-45-Steckverbinder zum Einsatz, die in der Netzwerktechnik weit verbreitet sind und daher leicht verf�gbar bzw. erweiterbar sind. Das betrifft haupts�chlich die einfache und wartungsfreie Montage von Slave-Modulen im Gesamtsystem des Aufbaus. 

**Keine Kompatibilit�t zu Ethernet-Switches/-Hubs**!

Die Belegung  der RJ-45-Buchse ist **propriet�r und inkompatibel zu Ethernet**. 

Konkret leisten muss die RJ45-Buchse:

- Masseverbindung
- Reserviert
- I�C-Clock (+3.3V LVTTL)
- I�C-Data (+3.3V LVTTL)
- +12V DC-Versorgungsspannung
- Reset (Low-Active, +3.3V LVTTL)
- Reserviert
- Reserviert

Somit wird sichergestellt, dass selbst bei Verklemmung des I�C-Busses, ein durch den I�C-Master gesteuertes Reset ausgel�st werden kann. Die restlichen Aufgaben sind Datentransport und Bereitstellung einer gemeinsamen Spannungsquelle f�r alle Slaves. Die handels�blichen Cat5-Kabel bieten f�r dieses kleine I�C-Bussystem auch den Vorteil einer recht hohen Abschirmung gegen�ber HF-Einstr�mungen, da die Adern paarweise geschirmt sind (Twisted-Pair). Damit sollte eine f�r PWM ausreichend hohe Taktung des I�C-Busses auch �ber mal 2-3m
hin gew�hrleistet sein.


I�C-Bus
^^^^^^^
Zur Kommunikation zwischen RaspberryPi und den angeschlossenen Verbrauchern dient der von Philips entwickelte I�C-Bus, der �hnlich wie der SPI-Bus zur Kommunikation zwischen IC auf und zwischen Leiterplatten dient (**I�C=Inter-Integrated-Circuits**). Aus diesem Design folgen ein paar ernsthafte Limitierungen:

- Der I�C-Bus ist **nicht differentiell**, d.h. es wird **nicht** wie etwa bei CAN- oder RS485 mit zwei Datenpotentialen (D+, D-) gearbeitet, deren Differenzspannung vom Empf�nger gebildet wird.
- I�C ist somit anf�llig f�r Gleichtaktst�rungen (z.B. Z�ndfunken), hat aufgrund der niedrigen (LV)TTL-Pegel eine begrenzte Reichweite und ben�tigt �hnlich wie die RS232 immer eine gemeinsame Masse als Bezugspotential.
- I�C ist ein **getakteter Bus**
- I�C ist ein Master-Slave-Bussystem 
- Anzahl Teilnehmer ist auf 127 begrenzt
- Datenbreite f�r Register ist im Durchschnitt bei 16-Bit (implementierungabh�ngig)
- Terminierung erforderlich
- Datenraten von bis zu 5Mbit/s m�glich
- serieller Bus (MSB-first �bertragung)

Diese Master-Slave-Busarchitektur erm�glicht es dem Master, zyklisch Werte vom Bus abzufragen
(**Polling**). Manche IC-Implementierungen erm�glichen zus�tzlich die Verwendung von externen Interrupt-Pins, welche OnChange-Ereignisse signalisieren k�nnen. Aufgrund der dadurch resultierenden Verdrahtungskomplexit�t bietet sich das allerdings nur in speziellen Anwendungsf�llen an, wo z.B. ein preiswerter und leistungsbegrenzter 8-Bit-Mikrocontroller (m�glicherweise mit Optimierung auf maximale Batterielaufzeit) aufgrund eigener Resourcenrestriktionen und anderen integrierten Funktionen nicht st�ndig auf den I�C-Bus pollen kann.

Aus der Perspektive des RaspberryPi als I�C-Master bietet sich I�C sehr an, da mit den **i2c-tools** und dem Linux-Kernel-Modul **i2c-bcm2708** eine sehr leistungsstarke und komfortable Schnittstelle zur Arbeit mit I�C bereit steht. Die sehr gute Linux-Unterst�tzung f�r I�C r�hrt u.a. historisch auch daher, dass viele Temperatur-Sensoren auf PC-Mainboards �ber dieses Protokoll adressiert wurden (Stichwort **lm-sensors**).

Die I�C-Slaves als Teilnehmer m�ssen mit **eindeutigen Adressen** kodiert sein. Zu diesem Zweck dienen beim MCP23017 die Pins A[0..2], wodurch sich 2�=8 Teilnehmer unterscheiden lassen. Die Slave-Adressierung wird durch den montierten DIP-Schalter durchgef�hrt.


Versorgung
^^^^^^^^^^
Die Spannungsversorgung ist einheitlich auf +12V DC sichergestellt. Dies zum Einen dem Leistungsteil geschuldet, dessen Verbraucher diese Spannung erfordern, zum Anderen bietet sich dieser Spannungslevel aufgrund der Versorgung durch Kfz-Netzteile etc. an. 
Eine wichtige Rolle f�r die Versorgungsspannung spielt der I�C-Bus, der zur Kommunikation zwischen dem RaspberryPi und den Busteilnehmern dient. I�C funktioniert im Gegensatz zu CAN-
Bus oder anderen Feldbussystemen wie RS-485 **nicht differenziell**. Das bedeutet in der Konsequenz, dass sowohl **eine gemeinsame Masse**, als auch **ein gemeinsames Versorgungpotential** notwendig ist.

Der Broadcom-ARM-Prozessor des RaspberryPi verwendet sowohl f�r GPIOs, als auch f�r SPI und I�C-Bus ein LVTTL-Pegel, d.h. +3.3V, welche sowohl f�r den I�C-Takt, als auch
f�r die I�C-Datenleitung gelten.

Somit ergibt sich in der Konsequenz, dass als kleinster gemeinsamer Nenner zwischen RaspberryPi und GPIO-Extender beide auf LVTTL betrieben werden sollten.

F�r diese Zwecke wird ein Low-Drop-Spannungsregler von Texas Instruments vom Typ **LM1117** (http://www.ti.com/lit/ds/symlink/lm1117.pdf) eingesetzt.