# react-native-wifi-module (Android)

A react-native module for viewing and connecting to Wifi networks on Android devices.

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

```
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

      ....
  }

  ......

}
```

### Example usage

```
var wifiModule = require('react-native-wifi-module')
```

Toast all networks:
```
wifiModule.toastAllNetworks();
```

Sign device into a specific network:
```
wifiModule.findAndConnect(ssid, password);
```

You can put all wifi networks into a ListView like this:
```
wifiModule.loadWifiList((wifiString) => {
var wifiArray = wifiString.split('SSID:');
this.setState({
  dataSource: this.state.dataSource.cloneWithRows(wifiArray),
     loaded: true,
     });
 },
 (msg) => {
     console.log(msg);
   },
 );
 ```

connectionStatus returns true or false depending on whether device is connected to wifi:
```
wifiModule.connectionStatus((isConnected) => {
  if (isConnected) {
    //Do something
  }
},
```


### Screenshots

* Version of the app which implements RNSimpleAlertDialogModule by lucas ferreira     


![Screenshot from a version of this app which implements RNSimpleAlertDialogModule by lucas ferreira](http://i.imgur.com/Es4V0Wk.png)

![Upon connecting](http://i.imgur.com/11G14hw.png)

![3](http://i.imgur.com/QSLSexh.png)
