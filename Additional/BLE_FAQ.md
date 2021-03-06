Read through our documentation and didn't find the answer you were looking for? Try our FAQ.

##Q: How can I make my BLE device interactive?

BLE devices become interactive when you provide a means of input (and write your program so that it reacts to these inputs). This can be local, like a button or a touchpad, or remote, like a mobile app or webpage. 

To learn about prototyping interactivity, see [here](/InDepth/Prototyping/).

##Q: How is a BLE beacon better than a QR code?

The main advantage of BLE beacons is that they're actively broadcasting to anyone in the area who's watching for BLEs; they don't require users to decide which QR code to scan. So long as users leave their BLE scanners working, which we can expect them to do more and more as BLE beacons come into wider use, they'll see all beacons in range automatically.

BLE beacons can also be hidden from view, unlike QR codes that need to be prominently displayed in an accessible location.

If you have BLE on an mbed board, you can also have an onboard interface, such as a screen or lights, to drive engagement.

##Q: Can I display the information locally?

If your hardware supports it (that is, has an external display). If you’re working with local display it’s best to show the raw data - processing the information before showing it will eat through your device’s battery.

Most platforms include LEDs, which are enough if you’re trying to indicate simple states such as connected/disconnected. 

##Q: I have a lot of information to send. What do I do?

BLE is short-range and designed for small bits of information. If you have a lot of information to show the user, it's more efficient to use BLE only to redirect the user to a webpage or application.

If it's a server you're trying to send to, you should use Ethernet or WiFi to communicate with it; mbed boards offer support for both.

If you still must send a large stream of data over BLE, you might want to shorten the connection interval and use write-without-response commands instead of a simple write. See [here](/AdvSamples/HighData/) for more information.

##Q: I have a lot of information to store. What do I do?

If you want a small and power-efficient device, you probably don't want to store too much locally; send your information to a server instead (it doesn't have to be a web server; it can be your own computer, if it's set up correctly).

BLE is a short-range method, meaning you'll be able to send information over BLE only if your device and your destination are quite close. If they're farther away, you'll need to use Ethernet (regular cable connection), WiFi or radio.

##Q: Can I use BLE beacons for geolocation?

If you're desperate enough. You can calculate how far away a mobile phone is from a beacon if you know how distance affects the signal strength. But there are a lot of other factors that affect signal strength, and you cannot predict or cancel them out. For example, if there is nothing between the phone and the BLE device, you'll get a stronger signal strength than if anything - including the person holding the phone - comes between them. So using one BLE device for geolocation will not give you accurate results.

If you have a lot of BLE devices scattered in the same space, and they're all measuring the signal strength of a single phone, you can get a far more accurate result by triangulating the phone's location. But this is probably not an efficient use of BLE devices, if for no other reason than that it requires a computer to do the actual triangulation, forcing you to give the BLE devices network access and hiking the price of the devices (they'll also eat through their batteries). 

##Q: Can I use BLE for location-based interactions?

Yes, if by location you mean "when a phone or other BLE-capable device comes within range of my BLE beacon".

##Q: Can a beacon reveal its location?

You can find a beacon by assuming that the stronger the signal, the closer you are to the source; move towards where the signal is strongest and you'll find the beacon, like a game of Marco Polo. The beacon could also explicitly reveal its location through its advertisement payload.

##Q: What is BLE's range, and can I extend or limit it?

Bluetooth signals have a limited range, with Class 2 devices limited to about ten meters (33 feet); this can be extended with an antenna. Signals can be blocked by concrete and metal, so they don't always travel through walls - making their room the extent of their range.

##Q: Is there a version limit for BLE?

BLE made its first appearance in 2010 with the adoption of the Bluetooth Core Specification Version 4.0 and is not supported on older mobile devices or tablets. However, since these devices are regularly replaced, and almost all new devices do support BLE, we can expect wide support in a year or two.

##Q: Can the BLE device talk to the internet?

At the moment, BLE devices don't have direct internet access. To get internet access, you can do one of two things:

1. You can give your board a secondary communication method, like Ethernet or WiFi. Do note that this can easily double the price of the board. 

2. The BLE device can get internet over its BLE connection to a mobile phone. That is: there could be phone apps that act as internet gateways for BLE devices. When the phone terminates the BLE connection, the BLE device will lose its internet access. This doesn't require additional hardware, so it doesn't affect the price of the board, but it does mean that for the device to have constant internet access it will need a phone (or BLE-enabled computer) next to it.

In the future, we may find routers that accept BLE connections, in the same way that they currently accept WiFi connections. This is already a part of the latest BLE standard, and should become available through mbed in the near future.

##Q: What's meshing, and does it work?

Mesh is a network topology in which each node relays data for the network, often using broadcasts. All nodes cooperate in the distribution of data in the network, making it somewhat independent from the need for centralised routing and more resilient to failures. Meshing is an effective way of sending small amounts of information from one BLE device to another, or from one device to a large array of devices. At the moment there's no easy way of doing it with BLE, since it requires enabling the scanning for advertisements in BLE peripherals; the mbed team is working on bringing this feature to BLE_API soon.

##Q: How can I use several BLE devices at once?

As we said, meshing isn't a workable option yet. But BLE devices on their own can all lead to a single place, like a web server, and that single place can aggregate all their information for storage, processing or interactivity. From there, you can control each one on its own, or several at once.

##Q: What's FOTA, and does it work?

FOTA stands for Firmware Over the Air, and is a method of updating the BLE device's programming remotely, rather than by physically connecting it to the computer. 

FOTA works (on the Nordic nRF51822 board), but at the moment it doesn’t come with security features to authenticate or verify new firmware. We’ll bring security into mbed FOTA during 2015.

_____

Still have questions? Ask [our community](https://developer.mbed.org/teams/Bluetooth-Low-Energy/community/).
