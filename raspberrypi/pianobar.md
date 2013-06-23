Title:Pianobar on the Pi!
Date: 2013-1-1 12:01

I installed pianobar on the pi! It was an arduous learning process but in the end some learning was actually accomplished. To be fair, pianobar was the easy part. A simple...

	:::console
	sudo apt-get install pianobar

was sufficient to get me up, running and finding errors. 

The first error I found was the classic TLS handshake
	
	:::console
	(i) Login... Network error: TLS handshake failed.

which can be fixed by finding the most up to date fingerprint and throwing it into the config file in home/pi/.config/pianobar

My config file sits at three lines right now...

	:::text
	user = me@mydomain.com
	password = asecret
	tls_fingerprint = 2D0AFDAFA16F4B5C0A43F3CB1D4752F9535507C0

Once I tire of Christmas music (never) I'll probably make my Coltrane station autostart with...

	:::text
	autostart_station = 123456

Until then I'll just manually choose my Christmas station each and every time. 

At that point pianobar was up and running smoothly. I didn't know it because I had a separate, darker issue prohibiting the Pi from sending audio over HDMI. But that's a story for another [post](|filename|/raspberrypi/berrybootconfig.md)

Possible improvements going forward include: starting pianobar at system startup, creating a nicer UI so my wife can use it.

