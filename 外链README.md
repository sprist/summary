#外链

1、AndroidManifest.xml配置

```java
        <activity
            android:name="com.rubik.ucemd.rubikwaplink.WapLinkMainActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucemd.rubikwaplink.BarCodeActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucemd.rubikwaplink.ErrorActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
```

2、Application配置

```java
public class AppPatientDemoContexts extends AppHttpContexts {

    @Override
    public void onCreate() {
        super.onCreate();
        AppHttpContexts.getAppContext().setWapLinkErrorActivity(ErrorActivity.class);
        AppHttpContexts.getAppContext().setWapLinkActivity(WapLinkMainActivity.class);
        AssetsUtils.initAsssets(this);
    }
 ｝
```
