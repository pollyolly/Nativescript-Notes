# To fix  Error : “Execution failed for task ':app:processDebugManifest'.” in NS5.1 to support Nativescript plugin firebase

Copy the code below in the app.gradle

project-folder/app/App_Resources/Android/app.gradle

```
dependencies {
    configurations.all {
          exclude group: 'commons-logging', module: 'commons-logging'
        resolutionStrategy.eachDependency { DependencyResolveDetails details ->
            def requested = details.requested
            if (requested.group == 'com.google.firebase') {
              details.useVersion '17.+'
            }
            if (requested.group == 'com.google.android.gms') {
                details.useVersion '16.+'
            }
            if (requested.group == 'com.android.support' && requested.name != 'multidex') {
                // com.android.support major version should match buildToolsVersion
                details.useVersion '28.+'
            }           
        }
    }
  }
```

# Setup Nativescript plugin firebase Android

Install

<pre>
npm install tns-platform-declarations
tns install typescript
</pre>

Create the file and add in project-folder/references.d.ts

```
/// <reference path="./node_modules/tns-platform-declarations/ios.d.ts" />
/// <reference path="./node_modules/tns-platform-declarations/android.d.ts" />
/// <reference path="./node_modules/nativescript-plugin-firebase/firebase.d.ts" />
```

Install the nativescript plugin firebase. 
```
tns plugin add nativescript-plugin-firebase
```
Answer (y) to 
```
prompt: Are you using Android (y/n): (y)
prompt: Are you using Firebase Cloud Messaging? (y/n): (n) y
prompt: Do you want to save the selected configuration. Reinstalling the dependency will reuse the setup from: firebase.nativescript.json. CI will be easier. (y/n): (y)
```
Generate the google-service.json in firebase then add to 
<pre>
project-folder/app/App_Resource/Android/
</pre>

Important:

<pre>
Device Token - generated when first initialize the firebase in your mobile app.
Server Key - click the Cloud Messaging in firebase and get the service key.
</pre>

Sample code to request notification.

```
sendFirebaseNotification: function(data){
		return new Promise((resolve, reject) => {
			http.request({
        		url: "https://fcm.googleapis.com/fcm/send",
            	method:"POST",
            	headers:{ 
					"Authorization": data.serverKey,
					"Content-Type": "application/json"
				 },
            	content: JSON.stringify({ 
					"notification": {
						"title": data.title,
						"text": data.text,
						"sound": "default",
						"android_channel_id": "fcm_default_channel"
					},
					"priority": "High",
					"to": data.deviceToken
				})
        	}).then((response) =>{
				console.log(response);
	        }, (error) => {
				reject(error);
        	});
	   });
	} 
```
Sample code for firebase
```
const firebase = require("nativescript-plugin-firebase");
firebase.init({
                showNotifications: true,
                showNotificationsWhenInForeground: true,
            onPushTokenReceivedCallback: (token) => {
                console.log('[Firebase] onPushTokenReceivedCallback:', { token });
                this.$store.dispatch("SET_DEVICE_TOKEN", token);
                this.$store.dispatch("SET_SERVER_KEY", serverKey);
            },
            onMessageReceivedCallback: (message) => {
                console.log('[Firebase] onMessageReceivedCallback:', { message });
            }}).then(() => {
                console.log('[Firebase] Initialized');
            }).catch(error => {
                console.log('[Firebase] Initialize', { error });
            });
```
Important in Firebase 
<pre>
Android package name - can be found in project-folder/package.json
</pre>

References:
<pre>
https://medium.com/@renzocastro/nativescript-push-notifications-with-firebase-cloud-messaging-2a4a8643a8cb
https://github.com/EddyVerbruggen/nativescript-plugin-firebase
https://github.com/NativeScript/NativeScript/issues/7372#issuecomment-509039191
</pre>
