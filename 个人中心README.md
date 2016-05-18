#个人中心

1、AndroidManifest.xml配置

```java
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserCenterActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserLoginActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserRegisterActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserSettingActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserFindPasswordActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserFeedBackActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.AboutMainActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucmed.rubikuser.UserUpdatePasswordActivity"
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
        AppUIContexts.getAppContext().setUserLoginActivity(UserLoginActivity.class);
        AppUIContexts.getAppContext().setUserCenterActivity(UserCenterActivity.class);
    }
 ｝
```
