#第三方模块(微信支付宝)

1、信鸽推送

Application配置

```java
public class AppPatientDemoContexts extends AppHttpContexts {
  @Override
    public void onCreate() {
        super.onCreate();
         initXG(this);
    }
    
    private void initXG(final Context context) {
        XGPushUtils.getInstance(context).setLogoutLinstener(new XGPushUtils.LogoutLinstener() {
            @Override
            public void LogoutRemind() {
                UserUtils.setLogin(false);
                UserUtils.reLogin(context);
            }
        }).setNewMessageLinstener(new XGPushUtils.NewMessageLinstener() {
            @Override
            public boolean NewMessage(Context context,
                                      PushReceiverMessage receiverMessage, Intent intent) {//配置相关方法
                intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP
                        | Intent.FLAG_ACTIVITY_SINGLE_TOP);
                ActivityMessageLife l = AppHttpContexts.getMessageLife();
                if (l != null && l.getMessageType() == WapLinkConfig.WAPACTIVITYPUSH) {
                    l.load(receiverMessage.json);
                } else {
                    intent.setClass(context, WapLinkMainActivity.class);
                    intent.putExtra("from", WapLinkConfig.PUSH_FROM);
                    return false;
                }
                return false;
            }
        });
        AppUserConfig.getInstance(context).setLoginSuccess(new AppUserConfig.LoginSuccess() {
            @Override
            public void Success(String pushAccount) {
                XGPushUtils.initXingePush(context, pushAccount);
            }
        });
    }
  }
```

AndroidManifest.xml配置

```java
 <!-- 信鸽推送 -->
        <!-- 【必须】 (2.30及以上版新增)展示通知的activity -->
        <activity
            android:name="com.tencent.android.tpush.XGPushActivity"
            android:exported="true"
            android:theme="@android:style/Theme.Translucent">
            <intent-filter>

                <!-- 若使用AndroidStudio，请设置android:name="android.intent.action" -->
                <action android:name="android.intent.action" />
            </intent-filter>
        </activity>

        <!-- 【必须】 信鸽receiver广播接收*****************************************************************************************************8 -->
        <receiver
            android:name="com.tencent.android.tpush.XGPushReceiver"
            android:exported="true"
            android:process=":xg_service_v2">
            <intent-filter android:priority="0x7fffffff">

                <!-- 【必须】 信鸽SDK的内部广播 -->
                <action android:name="com.tencent.android.tpush.action.SDK" />
                <action android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
                <!-- 【必须】 系统广播：开屏和网络切换 -->
                <action android:name="android.intent.action.USER_PRESENT" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

                <!-- 【可选】 一些常用的系统广播，增强信鸽service的复活机会，请根据需要选择。当然，你也可以添加APP自定义的一些广播让启动service -->
                <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
                <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
            </intent-filter>
            <!-- 【可选】 usb相关的系统广播，增强信鸽service的复活机会，请根据需要添加 -->
            <intent-filter android:priority="0x7fffffff">
                <action android:name="android.intent.action.MEDIA_UNMOUNTED" />
                <action android:name="android.intent.action.MEDIA_REMOVED" />
                <action android:name="android.intent.action.MEDIA_CHECKING" />
                <action android:name="android.intent.action.MEDIA_EJECT" />

                <data android:scheme="file" />
            </intent-filter>
        </receiver>
        <!-- 【必须】 信鸽service -->
        <service
            android:name="com.tencent.android.tpush.service.XGPushService"
            android:exported="true"
            android:persistent="true"
            android:process=":xg_service_v2" />
        <service
            android:name="com.tencent.android.tpush.rpc.XGRemoteService"
            android:exported="true">
            <intent-filter>

                <!-- 【必须】 请修改为当前APP包名.PUSH_ACTION -->
                <action android:name="${PACKAGE_NAME}.PUSH_ACTION" />
            </intent-filter>
        </service>

        <!-- 【可选】APP实现的Receiver，用于接收消息透传和操作结果的回调，请根据需要添加 -->
        <!-- YOUR_PACKAGE_PATH.CustomPushReceiver需要改为自己的Receiver： -->
        <receiver android:name="com.rubik.ucmed.toolbox.push.MessageReceiver">
            <intent-filter>

                <!-- 接收消息透传 -->
                <action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
                <!-- 监听注册、反注册、设置/删除标签、通知被点击等处理结果 -->
                <action android:name="com.tencent.android.tpush.action.FEEDBACK" />
            </intent-filter>
        </receiver>

        <!-- 【必须】 请修改为APP的AccessId，“21”开头的10位数字，中间没空格 -->
        <meta-data
            android:name="XG_V2_ACCESS_ID"
            android:value="${XG_V2_ACCESS_ID}" />

        <!-- 【必须】 请修改为APP的AccessKey，“A”开头的12位字符串，中间没空格 -->
        <meta-data
            android:name="XG_V2_ACCESS_KEY"
            android:value="${XG_V2_ACCESS_KEY}" />

        <!-- 【必须-信鸽Pro】 请将value改为MTA分配的appkey，如果是开平、互联、广点通用户，请直接填写为Aqc+开平appid，如：Aqc123456< -->
        <meta-data
            android:name="TA_APPKEY"
            android:value="AH11YUL57AKE" />

        <!-- 【必须-信鸽Pro】 请将value改为app发布的市场名称，如在应用宝就写：应用宝、play写play< -->
        <meta-data
            android:name="InstallChannel"
            android:value="play" />

```


