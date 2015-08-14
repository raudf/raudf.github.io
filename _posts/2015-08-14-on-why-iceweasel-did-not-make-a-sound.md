---
layout: post
title: On why Iceweasel didn't make a sound
---

Since I run debian 8, I had my browsing experience a little disminished.  
I'm a big fan of not having flash installed.  

I always had trouble with vimeo, and recently even youtube and other started to have issue.  
Some video would play, some wouldn't, but I never had sound.  
I would usually get a local copy anyway (going back and forth within a stream tend to break).  

Since I'm not really bothered, it was all good, well until today.  
I wanted to use [hubl.in](https://hubl.in) with my coworker but I couldn't hear them :/  
Despite the fact that looking at them is cool, it is not realy helping to communicate.

I knew the problem would be with my setup.  
I have 2 sounds cards, one being the default and one being the HDMI output.  
The problem is that the first one to be detected and enabled is the HDMI one.  

To get sound working for mplayer I had to do the follwoing.  
Create a ```/etc/asound.conf``` with the following:  
```
pcm.!default {
    type hw
    card 1
}

ctl.!default {
    type hw
    card 1
}
```

My default card is set to be the second one by order of apparition (0 being the first).  
That way when application look for it, they don't get the HDMI, but the card connected to my speaker instead.  

If we look at ```aplay -l``` the order is still wrong
```
**** List of PLAYBACK Hardware Devices ****
card 0: HDMI [HDA ATI HDMI], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: Generic [HD-Audio Generic], device 0: ALC269VB Analog [ALC269VB Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

With that in mind, I set myself to get the order right one layer above (or under if you prefer.)  
The next step is to trick the sound module into re-ordering the cards.

I looked around a bit and while it all looked complicated, the solution is quite simple.  
I edited (a then blank) ```/etc/modprobe.d/alsa-base.conf```
```
options snd_hda_intel index=1
```

That way the first card detected is put to the index one.  
Therefore the second card is able to take the index zero.  
That way, I don't need the ```/etc/asound.conf``` and ```aplay -l``` has the rigth order:
```
**** List of PLAYBACK Hardware Devices ****
card 0: Generic [HD-Audio Generic], device 0: ALC269VB Analog [ALC269VB Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: HDMI [HDA ATI HDMI], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

As usual, here is a film that I realy liked: [blindness](http://www.imdb.com/title/tt0861689/)
