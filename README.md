iBeacon
=======

iBeacon is the Apple Trademark[1] for an indoor positioning system[2][3][4][5] that Apple Inc. calls "a new class of low-powered, low-cost transmitters that can notify nearby iOS 7 devices of their presence."[6] The technology enables an iOS device or other hardware to send push notifications to iOS devices in close proximity. Android operating system devices can receive iBeacon advertisements but cannot emit iBeacon advertisements (ie. central role only[7]).[8]  The iBeacon works on Bluetooth Low Energy (BLE), also known as Bluetooth Smart. BLE can also be found on Bluetooth 4.0 devices that support dual mode.[9] One potential application is a location-aware, context-aware, pervasive small wireless sensor beacon that could pinpoint users' location in a store: iBeacons could send notifications of items nearby that are on sale or items customers may be looking for, and it could enable payments at the point of sale (POS) where customers don’t need to remove their wallets or cards to make payments. It could be a possible Near Field Communication (NFC) competitor.[citation needed]  It uses Bluetooth low energy Proximity sensing to transmit a Universally unique identifier[10] picked up by a compatible app or operating system that can be turned into a physical location[11] or trigger an action on the device[12] such as a Check-in on social media or a push notification.  Various vendors have made hardware iBeacons that come in a variety of form factors. This includes small coin cell and AA powered devices, USB sticks, and software versions using Bluetooth 4.0 capable USB dongles.[13] An assortment of iBeacon from different vendors  Contents      1 Functions         1.1 Region monitoring         1.2 Ranging         1.3 Settings     2 Latest developments     3 Technical details     4 Spoofing     5 Compatible devices     6 Comparable technologies     7 See also     8 References     9 External links  Functions  It is important to understand almost all of the logic behind an iBeacon deployment is through the supporting application on the devices (e.g. iBeacon aware apps on the cellphones). The only role of the iBeacon is to advertise to the phones of its own existence at the physical location. Contrary to common misunderstanding, iBeacon do not actively push out notifications (other than the iBeacon advertisement frames) nor does iBeacon actively track nearby users. The application on the supporting devices must handle all the logic after seeing nearby iBeacons. Client devices however can sometimes connect to the iBeacons to retrieve values from iBeacon's GATT service. Values of interest include battery level or manufacturer specific data. Region monitoring  Region monitoring is limited to 20 regions and can function in the background (of the listening device) and has different delegates to notify listening app (and user) of entry/exit in the region - even if app is in the background or phone is locked. Region monitoring also allows for a small window in which iOS gives a closed app an opportunity to react to the entry of a region. Ranging  Ranging works only in the foreground but will return (to the listening device) an array (unlimited) of all iBeacons found along with their properties (UUID, etc.) [14]  An iOS device receiving an iBeacon transmission can approximate the distance from the iBeacon. The distance (between transmitting iBeacon and receiving device) is categorised into 3 distinct ranges:[15]      Immediate: Within a few centimetres     Near: Within a couple of metres     Far: Greater than 10 metres away  An iBeacon broadcast has the ability to approximate when a user has entered, exited, or lingered in region. Depending on a customer's proximity to a beacon, they are able to receive different levels of interaction at each of these 3 ranges.[16]   The maximum range of an iBeacon transmission will depend on the location and placement, obstructions in the environment and where the device is being stored (e.g. in a leather handbag or with a thick case). Settings  The frequency of the iBeacon transmission depends on the configuration of the iBeacon and can be altered using device specific methods. Both the rate and the transmit power have an effect on the iBeacon battery life. iBeacons come with predefined settings and several of them can be changed by the developer. Amongst others the rate and the transmit power can be changed as well as the Major and Minor values. The Major and Minor values are settings which can be used if you want to connect to specific iBeacons or if you want to work with more than one iBeacon at the same time. Typically, multiple iBeacon deployment at a venue will share the same UUID, and use the major and minor pairs to segment and distinguish subspaces within the venue. You can for example set the Major values of all the iBeacons in a specific store to the same value and use the Minor value to identify a specific iBeacon within the store.[17]   Latest developments 	This section possibly contains unsourced predictions, speculative material, or accounts of events that might not occur. Please help improve it by removing unsourced speculative content. (December 2013)  In mid 2013 Apple introduced iBeacons and experts wrote about how it is designed to help the retail industry by simplifying payments and enabling on-site offers. With the launch of iOS 7, retailers and other small to medium enterprises will be able to use this Bluetooth 4.0 based technology. On December 6, 2013, it was reported that Apple activated iBeacons across its 254 US retail stores.[18]  As of May 2014, different hardware iBeacons can be purchased for as little as $5 per device to more than $30 per device. [19] Each of these different iBeacons have wildly varying default settings for their default transmit power and iBeacon advertisement frequency. Some hardware iBeacons advertise at as low as 1 Hz while others can be as fast as every 100ms.  iBeacon technology is still in its infancy, early adopters of this technology should be aware of software quirks running on the current handsets. One well reported software quirk exist on the latest Android system whereby the system's bluetooth stack crash when presented with many iBeacons. [20] Technical details  Bluetooth low energy devices can operate in an advertisement mode to notify nearby devices of its presence. [21] At the most simple form, an iBeacon is a Bluetooth low energy device emitting advertisement following a strict format, that being an Apple defined iBeacon prefix, followed by a variable UUID, and a major, minor pair. An example iBeacon advertisement frame could look like:   fb0b57a2-8228-44 cd-913a-94a122ba1206 Major 1 Minor 2  where fb0b57a2-8228-44 cd-913a-94a122ba1206 is the UUID. Since iBeacon advertisement is just an application of the general Bluetooth low energy advertisement, the above iBeacon can be emitted by issuing the following command on Linux to a supported Bluetooth 4 device on a modern kernel.[22]     hcitool -i hci0 cmd 0x08 0x0006 a0 00 a0 00 00 00 00 00 00 00 00 00 00 07 00    ################################## 02 01 1a 1a ff 4c 00 02 15  # Apple's fixed iBeacon advertising prefix    hcitool -i hci0 cmd 0x08 0x0008 1E 02 01 1A 1A FF 4C 00 02 15 FB 0B 57 A2 82 28 44 CD 91 3A 94 A1 22 BA 12 06 00 01 00 02 D1 00    hcitool -i hci0 cmd 0x08 0x000a 01  Spoofing  By design, the iBeacon advertisement frame is plain visible to any party that listens. This leaves the door open for interested parties to capture, copy and reproduce the iBeacon advertisement frames at different physical locations. This can be done simply by issuing the right sequence of commands to compatible Bluetooth 4.0 USB dongles. As of Feb 2014, successful spoofing of Apple store iBeacons have been reported. [23] This is not a security flaw in the iBeacon per se, but application developers must keep this in mind when designing their applications with iBeacons.  Listening for iBeacon can be achieved using the following commands with a modern Linux distribution:   hcitool -i hci0 lescan --passive  D6:EE:D4:16:ED:FC (unknown)  F6:BE:90:32:3C:5E (unknown)  ...  On another terminal, launch the protocol dump program:   hcidump -R -i hci0  > 04 3E 2A 02 01 00 01 FC ED 16 D4 EE D6 1E 02 01 06 1A FF 4C    00 02 15 B9 40 7F 30 F5 F8 46 6E AF F9 25 55 6B 57 FE 6D ED    FC D4 16 B6 B4  ...  The MAC address of the iBeacon alone with its iBeacon payload is clearly identifiable. The sequence of commands in Technical details can then be used to reproduce the iBeacon frame. Compatible devices      iOS devices with Bluetooth 4.0 (iPhone 4S and later, iPad (3rd generation) and later, iPad Mini (1st generation) and later, iPod Touch (5th generation).[24][25]     Android devices with Bluetooth 4.0 and Android 4.3 and later (Samsung Galaxy S3/S4/S4 Mini, Samsung Galaxy Note 2/3, HTC One, Google/LG Nexus 7 (2013 version)/Nexus 4/Nexus 5,[26] HTC Butterfly (aka Droid DNA).[27] and Moto G     Macintosh computers with OS X Mavericks (10.9) and Bluetooth 4.0   Comparable technologies  Although the NFC environment is very different and has many non-overlapping applications, it is still compared with iBeacons.      NFC range is up to 20 cm (7.87 inches) but the optimal range is &lt; 4 cm (1.57 inches). iBeacons have a significantly larger range.     NFC can be either passive or active. When using passive mode, the power is sent from the reader device. Whereas although Passif (bought by Apple Inc.) has worked on reducing the energy consumption, a battery pack is still needed inside iBeacon tags at this time.     Most smartphones ship with both Bluetooth 4.0 LE and NFC support but at this time, no iOS devices have been released with NFC support.
