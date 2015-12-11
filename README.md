# react-native-wifi-module

### Installation

```bash
npm install react-native-wifi-module --save
```

### Add it to your android project

* In `android/setting.gradle`

```gradle
...
include ':WifiModule', ':app'
project(':WifiModule').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-wifi-module')
```

* In `android/app/build.gradle`

```gradle
...
dependencies {
    ...
    compile project(':WifiModule')
}
```

* Register Module (in MainActivity.java)

```java
import com.ccmxy.wifimanager.WifiPackage;  // <--- import

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
      .addPackage(new WifiPackage()) // <------ add this line
      .setUseDeveloperSupport(BuildConfig.DEBUG)
      .setInitialLifecycleState(LifecycleState.RESUMED)
      .build();

      .......
  }

  ......

}
```
