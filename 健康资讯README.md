#健康资讯

1、AndroidManifest.xml配置

```java
        <activity
            android:name="com.rubik.ucemd.rubikarticle.ArticleMainActivity"
            android:configChanges="keyboardHidden|screenLayout"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
        <activity
            android:name="com.rubik.ucemd.rubikarticle.ArticleDetailActivity"
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
        AppUIContexts.getAppContext().setArticleMainActivity(ArticleMainActivity.class);
    }
 ｝
```
