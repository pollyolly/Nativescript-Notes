#To fix some errors in NS5.1
project-folder\app\App_Resources\Android\app.gradle

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


