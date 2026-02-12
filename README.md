# Unlock the Dell BIOS Advanced Mode (Without Windows)

*Last Updated: Feb 12, 2026*

On newer Dell laptops, the BIOS is very stripped-down by default, with options as essential as battery charging limits or virtualization support being hidden behind the "Advanced Mode."

I'm not sure exactly which laptops are affected, but if it was manufactured around 2025 and you're dealing with a similar problem as what I have described, you're probably at the right place.

If you don't run Windows, Dell as of Feb 2026 doesn't provide any official way of turning on Advanced Mode, at least as far as I can tell. But there is a working method, which I have aggregated here for those who might find it useful.

Following this guide will involve making changes to your BIOS, and therefore involves risk. This guide is a WORKAROUND. These changes will be made through Dell's enterprise software, but it is a piece of software which is not publicly listed anymore and may never be updated again. **You are ultimately responsible for what happens to your machine when you follow this guide**.

### Prerequisites
- Your Dell Laptop
- Ubuntu 24.04 flashed onto a USB drive

Does it have to be Ubuntu? Probably not, but that's the system Dell intended this software we are about to use to run on.

If you already run Ubuntu, then great! You don't even need the LiveUSB!

## Instructions

To get started, hop into that LiveUSB Ubuntu environment.

### Install Dell Command | Configure

Dell states that they officially support Ubuntu, and they've done an okay job keeping up with this commitment. As part of this support, Dell used to maintain a piece of software called **Dell Command | Configure**. Though intended for enterprise use, this software will be our ticket to unlocking the BIOS.

At some point recently, Dell must have discontinued work on the Ubuntu version of Dell Command | Configure, because it's no longer findable on their website without enlisting the help of the Wayback Machine. The download links themselves are still there, but no pages lead to them anymore.

Well, here's said link: [Get Dell Command | Configure (OFFICIAL)](https://www.dell.com/support/home/en-us/drivers/DriversDetails?driverId=V01T5)

In case Dell takes down the above page, I set up a Google Drive link: [Get Dell Command | Configure (UNOFFICIAL)](https://drive.google.com/file/d/1QuSVrDLKX3HXBh2YqaDyPPox48H3-Egh/view?usp=sharing)

No matter where you chose to download the software from, verify that the checksum is the following:
- MD5: `b7b5071a1625f7f2be18909d1ce55806`
- SHA1: `0e3b7fe3fb5aa2ffe93fe1d2298ee88bf37e7a94`
- SHA-256: `30ce838e4cff56e5422c71848e2f3c5ead2f215f807ea4248cd5f3e33a853adc`

Next, extract with tar and you should see two .deb packages and their respective signatures. 

Install them with dpkg: (`srvadmin-hapi` first)
```
sudo dpkg -i srvadmin-hapi_9.5.0_amd64.deb;
sudo dpkg -i command-configure_5.1.0-6.ubuntu24_amd64.deb
```

### Using the Program

Here's a [Manual](https://dl.dell.com/topicspdf/command-configure_users-guide4_en-us.pdf) I found for this program, which may or may not be useful, since it's for the Windows GUI version.

First, ensure the software is installed correctly by running:

`sudo /opt/dell/dcc/cctk`

And you should get output that looks like a bunch of commands. (flags)

There are lots of things you could change with this, but the one we care about is `--AdvancedMode`.

Run:

`sudo /opt/dell/dcc/cctk --AdvancedMode`

To read the value. It should be "AdvancedMode=Disabled".

To set it to enabled, simply run:

`sudo /opt/dell/dcc/cctk --AdvancedMode=Enabled`

It should also read the value, and say it is enabled.

Now, restart and go into your BIOS, it should look a little different now!

## Contributing

Please contribute if you have information about affected hardware!
