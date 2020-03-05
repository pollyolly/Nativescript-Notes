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
