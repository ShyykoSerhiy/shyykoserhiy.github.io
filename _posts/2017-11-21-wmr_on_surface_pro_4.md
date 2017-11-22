---
layout: post
comments: true
title: Using Windows Mixed Reality headset with Surface Pro 4 (or any other laptop with Intel© Iris™ Graphics 5xx card)
---

So you've finally received your Windows Mixed Reality headset that you've waited for so long only to find that your Surface Pro 4 doesn't go past compatibility check. This is what you probably see on your screen right now:
![Well that's unfortunate](/assets/2017-11-21/cant-run-mixed-reality.png)

Graphics driver 21.20.16.4627 (WDDM 2.1) ❌. Ok you probably can just update the driver, right? You can just go to Intel drivers site and download new driver, right? Nope, you can't do this ( at least at the moment when this article had been written you couldn't) and apparently neither Microsoft nor Intel are planning to add support for WDDM 2.2 for Iris Graphics cards in any immediate future [proof](https://communities.intel.com/thread/118761), [proof](https://answers.microsoft.com/en-us/surface/forum/surfpro4-surfupdate/windows-mixed-reality-on-the-surface-pro-4/fd823b4c-1351-48f0-98cc-bb0a299c592b). 

#Magical 'fix' that probably will stop working

Fortunately apparently you DON'T really need WDDM 2.2 to run Windows Mixed Reality, it works just fine on WDDM 2.1. All you need to do is tell Mixed Reality Portal that it's no big deal that you have some problems and your driver doesn't support WDDM 2.2.

In order to 'force' enable "NEXT" button event when your PC is supposedly not supported you need to make some changes in the registry. Disclaimer: I don't guarantee that this method will work for you. I have no idea if this may damage yours PC/Headset (it's not damaging my Surface as far as I can tell), but you should try this method only at your own risk. Stop here and wait for drivers if you are not ready.

#Regedit 

So you still want to try, do you? Let's start. Press "Windows + R", type "regedit" into the input and press "Enter".
This will open Registry Editor. Navigate to ```HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Holographic\FirstRun``` (just copy and paste this into the address bar at the top). Create a new DWORD (32-bit) value (via context menu) and name it ```AllowFailedSystemChecks```. Double click it and set the value to ```1```. 
![regedit](/assets/2017-11-21/regedit.png)

#Some other issues

That's it. Now You can restart Mixed Reality Portal and the "Next" button should be clickable. At this point, I was pretty confident that everything would work just fine. Mixed Reality Portal recognized my Samsung Odyssey headset,
and I had even set up boundaries. 
![odyssey](/assets/2017-11-21/odyssey.png)

But as soon as the Portal tutorial tried to start up my monitor began to flicker and no video displayed in the headset. The culprit was my cheap passive Mini DP to HDMI adapter. Microsoft has [recomended list](https://developer.microsoft.com/en-us/windows/mixed-reality/recommended_adapters_for_windows_mixed_reality_capable_pcs) of adapters that they recommend but as long as your adapter is an active one and supports 4k output it should be fine. I've bough [this one](https://www.amazon.ca/gp/product/B01MR11FFT/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1). With the proper adapter, everything finally began to work. 

#Performance

The overall experience in wmr on Surface Pro 4 is Ok. You for sure will not be able to game on it, but Cliff House experience works fine. Sometimes you can see some lag and controllers jitter a bit, but nothing critical. 