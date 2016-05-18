#版本更新

1、AndroidManifest.xml配置

         <service
            android:name="com.rubik.ucmed.systemupdatetool.services.UpdateService"
            android:exported="false" />
 
2、调用检测更新

  new UpdateUtils().update(Context context, boolean isShow);
