#动态模块

1、Applaction配置

```java
public class AppPatientDemoContexts extends AppHttpContexts {

    @Override
    public void onCreate() {
        super.onCreate();
        AppDynamicConfig.init(this);
    }
  }
```

2、DynamicFunctionUtils方法

```java
DynamicFunctionUtils.initHomeItems(Context context);//后台交互获取首页动态模块数据
DynamicFunctionUtils.storeHomeItems(String functions) ;//缓存首页动态模块数据
DynamicFunctionUtils.getHomeItems();//获取首页动态模块缓存数据
DynamicFunctionUtils.initUserItems(Context context, UserItemTask.LoadUserItemFinsh loadUserItemFinsh);//后台交互获取首页动态模块
DynamicFunctionUtils.storeUserItems(String functions);//缓存个人中心动态模块数据
DynamicFunctionUtils.getUserItems();//获取个人中心动态模块
DynamicFunctionUtils.getFunctionStyle();//获取软件默认风格
```

3、DynamicIntentUtils方法

```java
DynamicIntentUtils.functionIntent(Context context, ListItemFunction item);// 功能跳转
``` 

