Nativescript Tutorial using Keytool
```
https://www.nativescript.org/blog/steps-to-publish-your-nativescript-app-to-the-app-stores#step-7
```

Command line
```
tns build  android --release --env.aot --env.uglify --key-store-path IskoMo.jks --key-store-password myPassword --key-store-alias IskoMo --key-store-alias-password myPassword
```
Quick Tutorial using Android Studio

1. Generate KeyStore (.jks) in android studio
   Menu -> Build -> Generate Signed Bundle or APK -> (choose) APK ->
2. Then provide the keystore path, password, alias, and alias password.
3. Save the KeyStore (.jks)

Quick Tutorial using Nativescript Commandline

https://www.nativescript.org/blog/steps-to-publish-your-nativescript-app-to-the-app-stores#step-5

1. keytool -genkey -v -keystore iskomo.jks -keyalg RSA -keysize 2048 -validity 10000 -alias IskoMo
2. After answering questions migrate to 
3. keytool -importkeystore -srckeystore iskomo.jks -destkeystore iskomo.jks -deststoretype pkcs12
