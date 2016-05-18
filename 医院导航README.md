#医院导航

1、AndroidManifest.xml配置

```java
         <activity
            android:name="com.rubik.ucmed.rubiknavigation.HospitalNavigationActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubiknavigation.HospitalMapActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubiknavigation.HospitalNearbyActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubiknavigation.HospitalMapNearBySearchActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubiknavigation.HospitalRouteActivity"
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
        AppUIContexts.getAppContext().setHospitalMainActivity(HospitalNavigationActivity.class);
    }
 ｝
```
