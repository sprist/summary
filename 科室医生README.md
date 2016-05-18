#科室医生

1、AndroidManifest.xml配置

```java
        <activity
            android:name="com.rubik.ucemd.rubikdoctor.FacultyListActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucemd.rubikdoctor.DoctorListActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucemd.rubikdoctor.DoctorDetailActivity"
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
        AppUIContexts.getAppContext().setDoctorMainActivity(FacultyListActivity.class);
    }
 ｝
```
