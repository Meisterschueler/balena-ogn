
![balena OGN Glider Tracker](https://raw.githubusercontent.com/ketilmo/balena-ogn/master/docs/images/header.png)

**Feed the glider traffic in your area to the Open Glider Network (OGN) using a Raspberry Pi 3 or 4 with balena!**


Tracking commerical aircraft have since long become commonplace through popular services such as [FlightAware](https://flightaware.com/), [Flightradar24](https://www.flightradar24.com/), and [Plane Finder](https://planefinder.net/). Smaller soarding aircrafts such as gliders, paragliders and drones are not equiped with ADS-B transponders, however, and have been impossible to track. With Open Glider Network, that's changing. It's a community powered service that's tracking smaller aircraft using lightweight beacon technology such as FLARM, FANET and ADS-L. Sounds fun? All you need to start feeding data to Open Glider Network and OpenSky Network is a Rapberry Pi, an [RTL-SDR](https://www.rtl-sdr.com/) USB stick, and an antenna – together with the code and instructions below. 

# Stay in the loop

👉🏻&nbsp;<a href="https://buttondown.email/balena-ads-b"> Subscribe to our newsletter</a>&nbsp;👈🏻&nbsp; to stay updated on the latest development of this project and its sister project balena ADS-B Flight Tracker.

# Got stuck? Get help!

💬&nbsp; [Ask a question](https://github.com/ketilmo/balena-ogn/discussions) in our discussion board

🚨&nbsp; [Raise an issue](https://github.com/ketilmo/balena-ogn/issues) on GitHub

📨&nbsp; [Reach out directly](https://ketil.mo.land/contact)

🗞&nbsp; [Read past newsletters](https://buttondown.email/balena-ads-b/archive/)

# Supported devices
<table>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/intel-nuc.svg" alt="intel-nuc" style="max-width: 100%; margin: 0px 4px;"></td><td>Intel NUC</td>
</tr>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/jetson-nano-2gb-devkit.svg" alt="jetson-nano-2gb-devkit" style="max-width: 100%; margin: 0px 4px;"></td><td>Nvidia Jetson Nano 2GB Devkit SD</td>
</tr>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/raspberrypi3.svg" alt="raspberrypi3" style="max-width: 100%; margin: 0px 4px;"></td><td>Raspberry Pi 3 Model B+</td>
</tr>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/raspberrypi3-64.svg" alt="raspberrypi3-64" style="max-width: 100%; margin: 0px 4px;"></td><td>Raspberry Pi 3 (using 64bit OS)</td>
</tr>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/raspberrypi4-64.svg" alt="raspberrypi4-64" style="max-width: 100%; margin: 0px 4px;"></td><td>Raspberry Pi 4 (using 64bit OS)</td>
</tr>
<tr><td>
<img height="24px" src="https://raw.githubusercontent.com/ketilmo/balena-ads-b/master/docs/images/arch/raspberrypi5.svg" alt="raspberrypi5" style="max-width: 100%; margin: 0px 4px;"></td><td>Raspberry Pi 5</td>
</tr>
</table>

Please [let us know](https://github.com/ketilmo/balena-ogn/discussions/new) if you are successfully running balena-ogn on a hardware platform not listed here!

# Credits

The balena-ogn project was created and is maintained by [Ketil Moland Olsen](https://github.com/ketilmo/). It is based on the splendid [ogn-pi34](https://github.com/VirusPilot/ogn-pi34) repository maintained by the one and only [VirusPilot](https://github.com/VirusPilot). Thank you kindly for your great work! A big kudos also goes to the team behind Open Glider Network for making it all possible.

Software packages downloaded, installed, and configured by the balena-ogn script are disclosed in [CREDITS.md](https://github.com/ketilmo/balena-ads-b/blob/master/CREDITS.md).

# Contributors
<a href="https://github.com/ketilmo/balena-ogn/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=ketilmo/balena-ogn" />
</a>

# Table of Contents
Coming Soon!

# Part 1 – Build the receiver
In its most minimal configuration, the receiver can be built using three core components: A currently supported [device](https://thepihut.com/products/raspberry-pi-4-model-b?variant=20064052674622) (see the [complete list](#supported-devices) above), a good [RTL-SDR USB dongle](https://thepihut.com/products/rtl-sdr-blog-v3-usb-dongle-with-dipole-antenna-kit) and an [868 MHz](https://store.rakwireless.com/products/fiber-glass-antenna?variant=41100821921990) (for Europe, Africa, and New Zealand) or [915 MHz](https://store.rakwireless.com/products/fiber-glass-antenna?variant=39705894813894) (for USA and Australia) antenna. In addition, you would need a [power supply](https://thepihut.com/products/raspberry-pi-27w-usb-c-power-supply?variant=42531604136131) for the device, an [SD card](https://thepihut.com/products/sandisk-microsd-card-class-10-a1) to install the operating system on, an [antenna cable](https://store.rakwireless.com/products/pulsar-cable-rak9731-rak9733?variant=39677580968134), and – depending on your choice – an [SMA adapter](https://store.rakwireless.com/products/sma-adapter). If you don't have it already, you'll need a [SD card reader](https://thepihut.com/products/mini-usb-c-microsd-card-reader), too. Although not strictly necessary, a [case](https://thepihut.com/products/raspberry-pi-4-case) for the device could be a good idea.

Piecing together the pieces should be straightforward. For more information, including other antenna options, look at the official OGN [hardware docs](https://wiki.glidernet.org/ogn-receiver-hardware-and-software). (Remember: For balena-ogn to work, please go with a device from the [supported devices](#supported-devices) list.)



# Part 2 – Setup balena and configure the device

[![Deploy with button](https://www.balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/ketilmo/balena-ogn&defaultDeviceType=raspberrypi4-64)

or

 1. [Create a free balena account](https://dashboard.balena-cloud.com/signup). You will be asked to upload your public SSH key during the process. If you don't have a public SSH key yet, you can [create one](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
 2. Sign in to balena and head to the [*Fleets*](https://dashboard.balena-cloud.com/fleets) panel.
 3. Create a fleet with the name of your choice for your device type. Please take note of the fleet name. You will need it later. In the dialog that appears, pick a *Default Device Type* that matches your device. Specify the SSID and password if you want to use WiFi (and your device supports it). (If your device comes up without an active connection to the Internet, the `wifi-connect` container will create a network with a captive portal to connect to a local WiFi network. The SSID for the created hotspot is `balenaWiFi`, and the password is`balenaWiFi`. When connected, visit `http://192.168.42.1:8181/` in your web browser to set up the connection.
 4. balena will create an SD card image for you, which will start downloading automatically after a few seconds. Flash the image to an SD card using balena's dedicated tool [balenaEtcher](https://www.balena.io/etcher/).
 5. Insert the SD card in your receiver, and connect it to your cabled network (unless you plan to use WiFi only and configured that in step 3). 
 6. Power up the receiver.
 7. From the balena dashboard, navigate to the fleet you created. A new device with an automatically generated name should appear within a few minutes. Click on it to open it.
 8. Rename your device to your taste by clicking on the pencil icon next to the current device name.
 9. Next, we'll configure the receiver with its geographic location. Unless you know this by heart, you can use [Google Maps](https://maps.google.com) to find it. The corresponding coordinates should appear when you click on your desired location on the map. We are looking for the decimal coordinates, which should look like *60.395429, 5.325127.*
 10. Back in the balena console, verify that you have opened the view for your desired device. Click on the *Device Variables*-button. Add the following two variables: `LAT` *(Receiver Latitude)*, e.g. with a value such as `60.12345` and `LON` *(Receiver Longitude)*, e.g. with a value such as `4.12345`.
 11. Now, you're going to enter the receiver's altitude in *meters* above sea level in a new variable named `ALT`. If you need to find the altitude, you can find it using [one of several online services](https://www.maps.ie/coordinates.html). Remember to add the approximate number of corresponding meters if your antenna is mounted above ground level.
 12. Almost there! Next, we will push this code to your device through the balena cloud. We'll do that using the [balena CLI](https://github.com/balena-io/balena-cli). Follow the [official instructions](https://github.com/balena-io/balena-cli/blob/master/INSTALL.md) to download and install the CLI for your platform of choice.
 14. Head into your terminal and log in to balena with the following command: `balena login`. Then follow the instructions on the screen.
 15. Next, clone the balena-ads-b repository to your local computer: `git clone git@github.com:ketilmo/balena-ads-b.git`. If you want to make changes to the repo, you can also fork it.
 16. Head into the folder of the newly cloned repo by typing `cd balena-ads-b`.
 17. Do you remember your fleet name from earlier? Good. Now, we are ready to push the applications to balena's servers by typing `balena push YOUR–FLEET–NAME–HERE`.
 18. Now, wait while the Docker containers build on balena's servers. If the process is successful, you will see a beautiful piece of ASCII art depicting a unicorn right in your terminal window:
<pre>
			    \
			     \
			      \\
			       \\
			        >\/7
			    _.-(6'  \
			   (=___._/` \
			        )  \ |
			       /   / |
			      /    > /
			     j    < _\
			 _.-' :      ``.
			 \ r=._\        `.
			<`\\_  \         .`-.
			 \ r-7  `-. ._  ' .  `\
			  \`,      `-.`7  7)   )
			   \/         \|  \'  / `-._
			              ||    .'
			               \\  (
			                >\  >
			            ,.-' >.'
			           <.'_.''
			             <'

</pre>
 15. Wait a few moments while the Docker containers are deployed and installed on your device. The groundwork is now done – good job!


# Part 3 – Coming Soon


# Part 4 – Advanced configuration
## Disabling specific services
You can disable the balena-ogn services by creating a *Device Variable* named `DISABLED_SERVICES` with the services you want to disable as comma-separated values. For example, if you want to disable the ogn service, you set the `DISABLED_SERVICES` variable to `ogn`.


# Part 5 – Updating to the latest version
Updating to the latest version is trivial. If you installed balena-ads-b using the blue Deploy with balena-button, you can click it again and overwrite your current application. All settings will be preserved. For convenience, the button is right here:

[![Deploy with button](https://www.balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/ketilmo/balena-ogn&defaultDeviceType=raspberrypi4-64)

If you used the manual `balena push` method, pull the changes from the master branch and push the update to your application with the balena CLI. For complete instructions, look at [Part 2 – Setup balena and configure the device](#part-2--setup-balena-and-configure-the-device).

Enjoy!

![Visitors](https://api.visitorbadge.io/api/combined?path=https%3A%2F%2Fgithub.com%2Fketilmo%2Fbalena-ogn&countColor=%23263759)
