---
layout: post
title:  "Upload flutter projet on Google Play"
date:   2020-03-13 00:00:00 +0100
categories: technical code flutter mobile
---

Have you ever tried flutter? If not, I invite you to do it, it's worth a visit!

But did you go as far as publishing on stores and especially on Google Play?

I personally tried to publish an application made with this technology on Google Play but I found myself faced with an unexpected error:

![x64 Code Error](http://Kelvas09.github.io/assets/assets/img/posts/flutter_x64_googleplay/x64_error.png)

That's a problem!

Fortunately Android Studio allows us to compile for several platforms in the same APK but also to compile several APK, each for a different platform!

First of all, add the following code to your "app/build.gradle" file: 

```
    splits {
        abi {
            enable true
            reset()
            include "armeabi-v7a", "arm64-v8a"
            universalApk false
        }
    }
```

From there, at each compilation you will generate several APKs. One per platform, here **armeabi-v7a** and **arm64-v8a**.

Now you can start compiling for both platforms.

```
flutter build apk --release --target-platform=android-arm
```

An APK with the name **app-armeabi-v7a-release.apk** will be generated. Note that the 2 APKs will be generated each time but it is important to use only the one mentioned above.

Now increment the CodeVersion property of your project otherwise Google Play will refuse your new APK:

![Version Code Error](http://Kelvas09.github.io/assets/assets/img/posts/flutter_x64_googleplay/versionCode_error.png)

You can now generate the second APK with the command:

```
flutter build apk --release --target-platform=android-arm64
```

The new APK will be appointed **app-arm64-v8a-release.apk**.

The Google Play console should accept this second APK without any problem. Repeat the check and everything should work fine!

Also remember that it is essential to prepare for the future with the new APK x64.

So since this is a Google technology, we can imagine that a solution will be considered very soon!

I hope this article will get you more! Feel free to contact me to discuss further ;)