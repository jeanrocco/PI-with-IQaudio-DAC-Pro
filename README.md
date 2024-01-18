# PI-with-IQaudio-DAC-Pro
Play Spotify on a PI equipped with a IQaudio DAC Pro hat from any computer in your house, without the infamous Airplay(2) ...
###  It all started on april 20, 2023:
  
  I had just installed `Moode 8.3.1`, which comes with an Airplay2 renderer, on a `PI-3b 1.2` equipped with an `IQaudio DAC Pro` HAT. This was supposed to allow my 2 old mid-2012 MACs, recently upgraded with the wonderfull `https://dortania.github.io/OpenCore-Legacy-Patcher/`, to `VENTURA 13.3.1` no less, to stream music with Airplay2. The upgrade was justified by Airplay quitting unexpectedly on my older OSs. It felt like Apple was doing that on purpose with the older OS, but I'm not sure of that anymore, since I experienced Airplay's stutters and eventual shutdowns even with `VENTURA 13.3.1`.

  If you still want to try nice `Moode 8.3.1` anyway, [the push button to shutdown the PI and the led](https://github.com/jeanrocco/PI-shutdown-push-button/tree/master) work as before but in order to start the script at boot time you will have to add as root, at the end of  `/etc/rc.local`, and before `exit 0` : `(/home/pi/blink.py)&` as is, with the the parenthesis and the & symbol. . I got this from [`https://www.msldigital.com/pages/shutdown-scripts-for-moode-audio`](https://www.msldigital.com/pages/shutdown-scripts-for-moode-audio) . Blink.py is [here](https://github.com/jeanrocco/PI-shutdown-push-button/blob/master/blink.py.github) .

### UPDATE Nov. 2023: This update greatly simplify the previous setup, mostly meaning getting rid of obnoxious Airplay ...

  After some issues with the Airplay renderers, I found out a simpler, and most satisfying setup, based on Spotify's "connect to a device" feature, which allows to play tunes on the RPI IQaudio DAC, from another computer's browser.
  
  First install the latest PI OS on your PI. To make sure the IQaudio DAC is the default audio player comment out `dtparam=audio=on`, add `dtoverlay=iqaudio-dacplus` and `dtoverlay=vc4-kms-v3d,noaudio` in `/boot/config.txt:` 
```
...
...
# Enable audio (loads snd_bcm2835)
#dtparam=audio=on                       
dtoverlay=iqaudio-dacplus
#dtoverlay=rpi-dacpro

# Automatically load overlays for detected cameras
camera_auto_detect=1

# Automatically load overlays for detected DSI displays
display_auto_detect=1

# Enable DRM VC4 V3D driver
dtoverlay=vc4-kms-v3d,noaudio
max_framebuffers=2
...
...
``` 
One last thing, let's get rid of pulseaudio ... it breaks things ...
 
 `apt-get remove --purge pulseaudio`
 
 Reboot your PI, and from any PC or MAC, access it with VNC, and start a Chromium session to connect to the "Spotify web server" URL. Once connected to Spotify, test if it's playing on the DAC, then you can close the VNC session to your PI, if you want to, but don't close the Spotify web page. If you have no sound, type `alsamixer` and check that you have `Card: IQaudIODAC` as default `(pressing F6 and choosing - (default) always gives Card: IQaudIODAC)`.  
 
 Then on any PC or MAC computer, from any browser, again connect to the "spotify web server" URL, and at the bottom right hand corner, click the "speaker box like icon" displaying "connect to a device" and click "web player (Chrome)" which is still running on your PI. From now on, any tunes you choose will be played on the Pi's DAC ... ain't that cute !

 I'm using an ethernet cable for the PI to connect to my network, my WIFI isn't fast enough and I had stutters, UMMV.
 
 That's it, from any browser on any of your in house computer, you can now play music from gorgeous Spotify on the PI IQaudio DAC without the proprietary Airplays ...

 
 
  

### Enjoy !
jrb.
