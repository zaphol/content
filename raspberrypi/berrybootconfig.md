Title:The Joys and Frustrations of BerryBoot
Date: 2013-1-1 11:00

I tore open the wrapping paper on my RaspberryPi Christmas morning flush with excitement at this diminutive piece of PCB. As soon as I had the chance I grabbed my SD card and realizing my fancy new desktop had no card reader, ran straight to my 6 year old laptop and fired up the RaspberryPi.org beginner's guide. Since the windisk image program they recommended wouldn't work with my laptop I thought I would have to pass through a low-level hell to make my card bootable, at least until I stumbled across BerryBoot.

BerryBoot is the easiest way to get a Pi up and running. Download their .zip file, put it on your SD card, plug it into your Pi and power up! The BerryBootloader will pop up and ask you which OS you'd like to install. Since I had an 8GB card with ample room I opted for the standard Raspian and XBMC. It downloads, installs and runs. This stuff doesn't have to be hard.

It isn't always easy either. When I tried to run pianobar, a command line Pandora client, I could see it run but couldn't get any sound. If I booted into XBMC I had sound without a problem so I knew I had a software issue on my hands. 

The omniscient Google suggested a few culprits. 
	
1.My audio was muted/turned down

	:::console
	alsamixer

proved that my sound was not muted (press 'm') and my volume indeed turned up.

2.That I needed to fix my hdmi settings.

	:::console
	tvservice -s

helped check if my hdmi mode was set to hdmi (which can do sound) or DVI (which does not do sound). With help from [RPi Forums](http://www.raspberrypi.org/phpBB3/viewtopic.php?f=67&t=25933) I investigated further. Sure enough I was in DVI mode. So I tried to force audio over HDMI to no avail. 

The guys at [Element14](http://www.element14.com/community/thread/18205) got me halfway to a solution. I edited my boot config file in Raspian to try and force HDMI audio, only to have tvservice -s show me my efforts were futile. I was still in DVI mode. Clearly this was not the config file I was looking for. 

And all this brings me back to BerryBoot. After many frustrating, fruitless hours I finally thought to investigate that BerryBootloader screen. Sure enough, there are advanced options for each OS. One of those options is a boot config file where a well-placed hdmi_drive=2 can actually do some good. 

Now that I'm over the initial rage, it's actually a really nice feature to have a clear config file for each OS so easily accesible on boot. I'm sure it will make my future endeavors a little less rageful. It's already made them more musical.

