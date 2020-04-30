Unable to delete completely the database when uninstalling the application

```
and in <manifest> add:
    xmlns:tools="http://schemas.android.com/tools"

and in <application> add:
      android:allowBackup="false"
   		tools:replace="android:allowBackup"
```
