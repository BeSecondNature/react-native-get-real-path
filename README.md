## react-native-get-real-path

Get real file path from file uri

## Installation (iOS)

Currently No Support

## Installation (Android)

Make alterations to the following files:

* `android/settings.gradle`

```gradle
...
include ':react-native-get-real-path'
project(':react-native-get-real-path').projectDir = new File(settingsDir, '../node_modules/react-native-get-real-path/android')
```

* `android/app/build.gradle`

```gradle
...
dependencies {
    ...
    compile project(':react-native-get-real-path')
}
```

* register module (in MainActivity.java)

  * For react-native below 0.19.0 (use `cat ./node_modules/react-native/package.json | grep version`)

```java
import com.rngrp.RNGRPPackage;  // <--- import

public class MainActivity extends Activity implements DefaultHardwareBackBtnHandler {

  ......

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    mReactRootView = new ReactRootView(this);

    mReactInstanceManager = ReactInstanceManager.builder()
      .setApplication(getApplication())
      .setBundleAssetName("index.android.bundle")
      .setJSMainModuleName("index.android")
      .addPackage(new MainReactPackage())
      .addPackage(new RNGRPPackage())      // <------- add package
      .setUseDeveloperSupport(BuildConfig.DEBUG)
      .setInitialLifecycleState(LifecycleState.RESUMED)
      .build();

    mReactRootView.startReactApplication(mReactInstanceManager, "ExampleRN", null);

    setContentView(mReactRootView);
  }

  ......

}
```

  * For react-native 0.19.0 and higher
```java
import com.rnfs.RNGRPPackage; // <------- add package

public class MainActivity extends ReactActivity {
   // ...
    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
        new MainReactPackage(), // <---- add comma
        new RNGRPPackage() // <---------- add package
      );
    }
```

## Example usage (Android only)

```javascript
// require the module
var RNGRP = require('react-native-get-real-path');

RNGRP.getRealPathFromURI(fileUri).then(filePath =>
  console.log(path)
)
```

