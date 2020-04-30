Unable to delete completely the database when uninstalling the application

In manifest tag add
```
<manifest 
    xmlns:tools="http://schemas.android.com/tools"
```
and in application tag add
```
<application
      android:allowBackup="false"
   		tools:replace="android:allowBackup"
```
