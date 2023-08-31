---
title: Android Fingerprinting With Wallpapers
date: 2023-08-30 12:00:00 +0800
categories: [Android]
tags: [android, privacy, fingerprinting]     # TAG names should always be lowercase
toc: true
---

# Deanonymizing Android Users 
With the rise of Android as a privacy respecting operating system, especially with the promotion of GrapheneOS and LineageOS ROMs, it may be thought that identification of users has become harder, and while that is partially true, information on the methods to deanonymizing is somewhat scarce. There are a variety of methods, which I will explain, but the main takeaway is that while more secure and private operating systems provide protection, there are many vulnerabilities in concern to privacy. 

# Android 8.1 and Earlier
Custom wallpapers are a common aspect of Android phones that are able to provide surprising amounts of data on the user of the phone, without special permissions. For Android versions up to 8.1, applications had read access to the wallpaper image, providing vast quantities of information depending on the set wallpaper. For example, a wallpaper of a selfie of owner’s face or a picture of their friends allowed for collection of personal data through the `[getDrawableCall()]`,as the command produced a byte array, which could be used to restore the original image.

# Android 8.1 and later
Fortunately, in devices running Android 8.1 and later, the call now requires the permission to read the external storage, but a second call - introduced to compensate for the extra permissions - `[getWallpaperColors()]` provides a somewhat similar, although more restrictive method to link users. This call provides the three most common hues from a wallpaper, which are generated by [WallpaperManager] upon setting of the lock and/or system (home) screen. The three colors; primary, secondary and tertiary, are set by a variational K-means quantifier and provided to applications with the [getWallpaperColors()] call. As introduced in the Material You update (Android 12 and up), this information is meant to be used to match application and system themes to the theme of the wallpaper. However, the information on these three hues are excellent for fingerprinting, as there is a great diversity of wallpapers. 

# The Math
For each of the three most common hues, there are 256 combinations for each RGB value, for a total of 2^24 combinations per color. With three colors per image, there are are 2^72 possible values, for maximum of 2^144 combinations (with 2 different wallpapers). This information is provided as 144 bits, which can be used as a direct identifer, or inputed to create a SHA-256 hash, as in the case of the trial application created by Fingerprint. The application compares the hashes to other submitted hashes to determine the uniqueness or the device based solely on the wallpaper. Thankfully, such fingerprinting is defeatable - as explained by Fingerprint – by keeping the default wallpaper, or setting it to completely black (as in the case of GrapheneOS) to provide anonymity. You can try the application and read more [here](https://fingerprint.com/blog/how-android-wallpaper-images-threaten-privacy/).