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

### Example usage

```
var wifiModule = require('react-native-wifi-module')
//Toast all networks:
wifiModule.toastAllNetworks();

//Sign device into a specific network:
wifiModule.findAndConnect(ssid, password);

//Get toasted with details about a network with a specific SSID:
wifiModule.toastThisNetwork(ssid);

//Put all wifi networks into a ListView:
wifiModule.loadWifiList("", (wifiString) => {
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

//Find out if device is currently connect to wifi:
wifiModule.checkIfConnected();
```


### Screenshots

* Screenshot from [this implementation,](https://github.com/ccmxy/react-native-wifi-manager-android) taken after a list item was tapped
![This appears when you tap the name of the network](http://i.imgur.com/nPjvpet.png "Screenshot from this app")

* Version of the app which implements RNSimpleAlertDialogModule by lucas ferreira
![Screenshot from a version of this app which implements RNSimpleAlertDialogModule by lucas ferreira](http://i.imgur.com/7FIyUoD.png "Connect version 1")

* Upon successful connection with ```wifiModule.findAndConnect(ssid, password);```
![Upon connecting](http://i.imgur.com/xXfNzBR.png "Connect version 2")
