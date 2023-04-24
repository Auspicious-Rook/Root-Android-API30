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
