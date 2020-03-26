Nativescript Tutorial using Keytool
```
https://www.nativescript.org/blog/steps-to-publish-your-nativescript-app-to-the-app-stores#step-7
```

Command line
```
tns build  android 
		--release 
		--env.aot 
		--env.uglify 
		--key-store-path /home/updilc/Desktop/APK-OUTPUT/KeyStore/IskoMo.jks 
		--key-store-password myPassword
		--key-store-alias IskoMo 
		--key-store-alias-password myPassword
```
Quick Tutorial using Android Studio

1. Generate KeyStore (.jks) in android studio
   Menu -> Build -> Generate Signed Bundle or APK -> (choose) APK ->
2. Then provide the keystore path, password, alias, and alias password.
3. Save the KeyStore (.jks)

Quick Tutorial using Nativescript Commandline

https://www.nativescript.org/blog/steps-to-publish-your-nativescript-app-to-the-app-stores#step-5
