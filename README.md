# Root-Android-API30
A repro that has all the information and apps needed to root an Android API 30 emulated device.

I have created this repo as a place to come get an Android API30 emulator device rooted with Google Play installed for penetration testing. All the tools and aplications here are from others. This is just a quick walkthrough on how to root the device.

1. Install Android Studio. This guide is geared towards macOS but it is a similar process for Linux.
2. Clone or copy the file I have for rootAVD.  This is a series of scripts that automates the rooting process. The github is https://github.com/newbit1/rootAVD.
3. Clone or copy the file I have for EdXposed. This application allows you to install TrustMeAlready which will help bypass SSL cert pinning. The github is https://github.com/ElderDrivers/EdXposed.
4. Clone or copy the file I have for TrustMeAlready. This will be loaded later by EdXposed to bypass SSL cert pinning. The github is https://github.com/ViRb3/TrustMeAlready.
5. Clone or copy the file I have for Riru. Ensure that it is v 23.9. I know the latest version gave me issues. The github for 23.9 is https://github.com/RikkaApps/Riru/releases/tag/v23.9.
6. Open Andriod Studio and create a device. Be sure to Select Pixel 2 with the Android stoe symbol next to it.
![Screenshot 2023-04-24 at 10 09 05 AM](https://user-images.githubusercontent.com/130098009/234039076-010b91a4-fe37-4be8-a35c-0ab7b58eb0fb.png)
7. Select R, API 30, ARM64-v8 for macOS or x86-64 for PC, Android 11 (Google Play).
![Screenshot 2023-04-24 at 10 12 59 AM](https://user-images.githubusercontent.com/130098009/234040328-337b01d3-2744-4cdc-8bc5-22555b65c92a.png)
8. Start the emulator.
![Screenshot 2023-04-24 at 10 18 01 AM](https://user-images.githubusercontent.com/130098009/234041096-1af3ddb4-80a9-47ad-9a27-985167f2c5d1.png)
9. Put the device in developer mode. On the emulated device, got to settings, about emulated device, and scroll to the bottom where it shows the build nu,ber. Click on the build number 7 times to put the device into developer mode.
![Screenshot 2023-04-24 at 10 20 35 AM](https://user-images.githubusercontent.com/130098009/234041707-1713ee1e-b394-460e-8076-9591032e7d93.png)
10. Go to Settings, System, Advanced, Developer Options. Ensure that USB Debugging is enabled. I also turn off the adb authorizatioin timeout.
11. Ensure that the Android SDK is installed. In a terminal browse to /Users/(YOUR-USER)/Library/Android/sdk/platform-tools for macOS or TODO for Linux. run. Run `./adb shell` to ensure that you can connect to the running emulator.
12. Exit adb and change directories to where rootavd is at.
13. Run `./rootAVD.sh ListAllAVDs`
![Screenshot 2023-04-24 at 10 20 35 AM](https://user-images.githubusercontent.com/130098009/234045221-00a3aa46-8247-4f3c-a9a2-1fe2453cf7ef.png)
14. Run the code that looks similar to this (Note your path may be different) `./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/arm64-v8a/ramdisk.img` (Yours may be x86-64 if on PC).
15. It may give an error that adb is not on path. Add the adb to path via `export PATH=~/Library/Android/sdk/platform-tools:$PATH` (Your command may differ but rootAVD should give the right command for your platform)
16. Once the command hass ran succesffully it should look like the picture below.
![Screenshot 2023-04-24 at 10 39 25 AM](https://user-images.githubusercontent.com/130098009/234047010-43cdd220-c57b-4ccc-86d7-e8f96fcf911e.png)
17.Stop the emulated device if it did not reset itself. My has not. I had to go to the terminial and kill the emulator. I then exit out of Android Studio and run the emulator for the command line after adding it to my path. `export PATH=~/Library/Android/sdk/emulator:$PATH`
18. After adding the emulator to your path, run the command `emulator -writable-system -avd EMULATOR-NAME`
19. Open you apps on the emulated device and find Magisk. It will say a reboot is required and reboot your device. 
20. OPen Magisk again after the reboot.  Click on Install and then direct install.
![Screenshot 2023-04-24 at 10 51 30 AM](https://user-images.githubusercontent.com/130098009/234050001-5a156d36-6a95-4973-af03-6a7a8dd16b22.png)
![Screenshot 2023-04-24 at 10 52 00 AM](https://user-images.githubusercontent.com/130098009/234050210-1d813817-8fbf-4826-8bf9-ce9f11c7f065.png)
21. Your device should reboot. On the emulated device, browse to https://github.com/RikkaApps/Riru/releases/tag/v23.9 and download the v23.9 zip file.
22. Go back to the Magisk app, click on modules, Install form storage, and install the riru app. The device will reboot.
23. On the emulated device, browse to https://github.com/ElderDrivers/EdXposed/releases/tag/v0.5.2.2 and download the master release zip.
24. On the emulated device, browse to https://github.com/ViRb3/TrustMeAlready/releases/tag/v1.11 and download the TrustMeAlready apk.
25. Go back to the Magisk app, click on modules, Install form storage, and install the riru app. The device will reboot. Repeat this for EdXposed as well.
![Screenshot 2023-04-24 at 10 52 00 AM](https://user-images.githubusercontent.com/130098009/234052492-76bed0e7-d762-4b61-8d8e-153001cf9565.png)
26. Open up EdXposed, and go to modules, switch on the TrustMeALready app.
![Screenshot 2023-04-24 at 11 09 44 AM](https://user-images.githubusercontent.com/130098009/234054491-60371c8e-ea09-44ba-802d-ee5aff99002f.png)
27. Click the three elipses up top right and reboot to system



