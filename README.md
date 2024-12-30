# How to Root a Production Build Android Emulator

I have created this repo to remind myself on how to get an Android API 30 emulated device rooted with Google Play installed for penetration testing. All the tools and applications here are from others. This is just a quick walkthrough that puts it all together so that I do not forget in the future. The goal of this readme is to provide a complete walkthrough on how to set up an emulated Android device for penetration testing production environment application from the Google Play App Store. This guide should result in an emulated Android device that is rooted, has SSL bypass installed, and has an active Frida server running on the device. NOTE: If you download the frida server provided here, your frida server may not work. Frida often changes versions and the host and emulated device versions must be close to the same. The other files provided are specific versions required that are known to work together. I prefer to download them locally on the emulated device, but I have provided them here in case they get taken offline.

## Requirements

Have Android SDK installed on your host.

Have frida-tools installed on you host. `pip install frida-tools`

## Create the Emulator

1. Install Android Studio. This guide is geared towards macOS but it is a similar process for Linux.
2. Clone the repro from github or copy the files I have for rootAVD.  This is a series of scripts that automates the rooting process. The github is https://github.com/newbit1/rootAVD.
3. Open Andriod Studio and create a device. Be sure to Select Pixel 2 with the Google Play Store symbol next to it.

![Screenshot 2023-04-24 at 10 09 05 AM](https://user-images.githubusercontent.com/130098009/234039076-010b91a4-fe37-4be8-a35c-0ab7b58eb0fb.png)

4. Select R, API 30, ARM64-v8 for arm devices or x86-64 for x86-64, Android 11 (Google Play).

![Screenshot 2023-04-24 at 10 12 59 AM](https://user-images.githubusercontent.com/130098009/234040328-337b01d3-2744-4cdc-8bc5-22555b65c92a.png)

5. Start the emulator.

![Screenshot 2023-04-24 at 10 18 01 AM](https://user-images.githubusercontent.com/130098009/234041096-1af3ddb4-80a9-47ad-9a27-985167f2c5d1.png)

6. Put the device in developer mode. On the emulated device, go to settings, about emulated device, and scroll to the bottom where it shows the build number. Click on the build number 7 times to put the device into developer mode.

![Screenshot 2023-04-24 at 10 20 35 AM](https://user-images.githubusercontent.com/130098009/234041707-1713ee1e-b394-460e-8076-9591032e7d93.png)

## Root the Emulator with rootAVD

7. Go to Settings, System, Advanced, Developer Options. Ensure that USB Debugging is enabled. I also turn off the adb authorizatioin timeout.
8. Ensure that the Android SDK is installed. In a terminal browse to /Users/(YOUR-USER)/Library/Android/sdk/platform-tools for macOS or TODO for Linux. run. Run `./adb shell` to ensure that you can connect to the running emulator. Alternatively, you can add this program to your path.
9. Exit adb and change directories to where rootAVD is at.
10. Run `./rootAVD.sh ListAllAVDs`

![Screenshot 2023-04-24 at 10 33 37 AM](https://user-images.githubusercontent.com/130098009/234115189-ead22922-d8fc-4a7c-9d3e-bb15b0cc2125.png)

11. Run the code that looks similar to this (Note your path may be different) `./rootAVD.sh ~/Library/Android/sdk/system-images/android-30/google_apis_playstore/arm64-v8a/ramdisk.img` (Yours may be x86-64 if on PC).
12. It may give an error that adb is not on path. Add the adb to path via `export PATH=~/Library/Android/sdk/platform-tools:$PATH` (Your command may differ but rootAVD should give the right command for your platform)
13. Once the command has ran successfully, it should look like the picture below.

![Screenshot 2023-04-24 at 10 39 25 AM](https://user-images.githubusercontent.com/130098009/234047010-43cdd220-c57b-4ccc-86d7-e8f96fcf911e.png)

14. Stop the emulated device if it did not reset itself. Mine historically has not, and I had to go to the terminial and kill the emulator. I then exit out of Android Studio and run the emulator with the command line after adding it to my path because it just seems easier. `export PATH=~/Library/Android/sdk/emulator:$PATH`.
15. After adding the emulator to your path, run the command `emulator -writable-system -avd EMULATOR-NAME`.
16. Open you apps on the emulated device and find Magisk. It will say a reboot is required and reboot your device.
17. Open Magisk again after the reboot.  Click on Install and then direct install.

![Screenshot 2023-04-24 at 10 51 30 AM](https://user-images.githubusercontent.com/130098009/234050001-5a156d36-6a95-4973-af03-6a7a8dd16b22.png)

![Screenshot 2023-04-24 at 10 52 00 AM](https://user-images.githubusercontent.com/130098009/234050210-1d813817-8fbf-4826-8bf9-ce9f11c7f065.png)

## Download and Install Required Applications

18. Your device should reboot. On the emulated device, browse to https://github.com/RikkaApps/Riru/releases/tag/v23.9 and download the v23.9 zip file. NOTE:The latest release will not work, I know 23.9 will.
19. On the emulated device, browse to https://github.com/ElderDrivers/EdXposed/releases/tag/v0.5.2.2 and download the master release zip.
20. On the emulated device, browse to https://github.com/ViRb3/TrustMeAlready/releases/tag/v1.11 and download the TrustMeAlready apk.
21. Go back to the Magisk app, click on modules, install form storage, and install the Riru zip. The device will reboot. Repeat this for the EdXposed  zip as well.

![Screenshot 2023-04-24 at 11 01 43 AM](https://user-images.githubusercontent.com/130098009/234115591-54bda8c3-752e-4189-9c4a-c87d332cc676.png)

22. Open up EdXposed, and go to modules, switch on the TrustMeAlready app.

![Screenshot 2023-04-24 at 11 09 50 AM](https://user-images.githubusercontent.com/130098009/234097648-cda12318-621f-42c7-a5bd-c086ff4d4ca5.png)

23. Click the three elipses up top right and reboot to system
24. Open up a terminal and start the adb with the command `adb shell`
25. Once you have a shell on the emulator, type `su`. This will pull up a promt on the emulated device to allow root. Select yes. Run `whoami` to make sure you are root.
26. Open the Magisk app and click on super user at the bottom. (If you did not select allow root in time for the shell , then here is where you can also select it) Turn on super user for the shell as well as EdXposed.

![Screenshot 2023-04-24 at 2 27 21 PM](https://user-images.githubusercontent.com/130098009/234096348-71a0e86b-6d4d-49b7-bffd-99b4820f4b9f.png)

## Install and Start the Frida Server

27. On the host computer, browse to https://github.com/frida/frida/releases and download the latest frida-server-android-YOUR_EMULATOR_ARCH.xz.
28. Extract this file. In macOS just use the finder app, in Linux use the command `unxz frida-server.xz`.
29. Ensure adb is still in you path and then edit and use the command `adb push /PATH_TO/frida-server-VERSION-android-ARCH /data/local/tmp/`.
30. Edit then use the command `adb shell "chmod 755 /data/local/tmp/frida-server-VERSION-android-ARCH`.
31. Go back to your root shell via adb on the emulated device.
32. Ensure you are root or `su` to get root. Execute the command `/data/local/tmp/frida-server-16.0.18-android-arm64 &`. This will open a frida server on the emulated device to hook into with tools such as Objection.
33. Enjoy your rooted device with SSL bypass and frida-server installed and running! See below for some useful commands and how to proxy your device to burp.


# Tips


When running the emulator, I put the emulator on my path and use the command `emulator -writable-system -avd EMULATOR_NAME -http-proxy BURP_HOST_IP:PORT`. I use this to proxy my emulator through Burp on my Kali linux VM.

In burp, add a proxy listener and bind it to the port used in the above command and then select all interfaces. This should allow you to intercept all traffic. A Burp certificate install is not required due to the TrustMeAlready app!

![Screenshot 2023-04-24 at 3 40 43 PM](https://user-images.githubusercontent.com/130098009/234112398-04858390-2e95-4431-b943-cf80dab6cbee.png)

Frida Server will not work if the versions do not match up on the emulated device and the host computer. They change frequently so ensure that both are up to date if you are getting errors

# Mobile App Penetration Testing Tips


TODO


