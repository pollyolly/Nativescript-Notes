https://docs.nativescript.org/core-concepts/project-structure-app#apppackagejson

Catch Native application error to prevent application from crash

```
const application = require("tns-core-modules/application");

application.on(application.discardedErrorEvent, function (args) {
    const error = args.error;

    console.log("Received discarded exception: ");
    console.log(error.message);
    console.log(error.stackTrace);
    console.log(error.nativeException);
    //report the exception in your analytics solution here
});

application.on(application.uncaughtErrorEvent, function (args) {
  if (args.android) {
      // For Android applications, args.android is an NativeScriptError.
      console.log("NativeScriptError: " + args.android);
  } else if (args.ios) {
      // For iOS applications, args.ios is NativeScriptError.
      console.log("NativeScriptError: " + args.ios);
  }
});
```
Vuex

```
strict: false
```
