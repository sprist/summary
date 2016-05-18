#HTTP

1、Application配置

```java
public class AppPatientDemoContexts extends AppHttpContexts {

    @Override
    public void onCreate() {
        super.onCreate();
        initUrl("http://192.168.0.12:8080/api/exec/3fba2d7e-6a59-492d-a6d1-b56538ccedf4.htm", true);
    }
    
      @Override
    public RequestFail getRequestFail() {
        return new RequestFail() {
            @Override
            public void fail(boolean isFinish, Activity activity, int code, String... messages) {
                Toaster.show(activity, messages[0]);//交互失败异常处理
            }
        };
    }
 ｝
```


2、Activity继承BaseLoadingActivity<T>类

3、请求类

```java
  new RequestBuilder(this);//请求返回model
  new RequestPagerBuilder(this);//请求返回列表
  new RequestFileBuilder(this);//上传文件
```

4、请求返回model更多配置

```java
.api(String api)//配置api名字
.param(String key, Object value)//配置入参
.setParse(String key, Class<?> clazz)//解析model
.setParse(RequestParse parse)//自定义解析model
.setRequestFinish(RequestFinish requestFinish)//自定义请求成功调用方法
.ok(int resid)//请求成功提示文字 默认无
.error(int resid)//请求失败提示文字 默认提示出错信息
.setRequestHttpException(RequestHttpException requestHttpException）//自定义请求交互异常
.requestIndex()//发起请求
```

请求单个model实例

```java
 new RequestBuilder(this).api("Z002003").param("id", id).setParse("model", ArticleDetailModel.class).requestIndex();
```

自定义解析model实例

```java
 new RequestBuilder(this).api("Z002003").param("id", id).setParse(new RequestBuilder.RequestParse() {
                @Override
                public ArticleDetailModel parse(JSONObject obj) {
                 JSONObject news = obj.optJSONObject("news");
                 return  ParseUtil.parse(news, ArticleDetailModel.class);
                }
            }).requestIndex();
```

5、请求返回列表更多配置

```java
.api(String api)//配置api名字
.param(String key, Object value)//配置入参
.setPageSize(int pageSize//配置请求返回数量
.all(boolean isAll)//全部获取
.setParse(String key, Class<?> clazz)//解析model
.setParse(RequestParse parse)//自定义解析model
.setRequestFinish(RequestFinish requestFinish)//自定义请求成功调用方法
.ok(int resid)//请求成功提示文字 默认无
.error(int resid)//请求失败提示文字 默认提示出错信息
.setRequestHttpException(RequestHttpException requestHttpException）//自定义请求交互异常
.requestIndex()//发起请求
.requestNext()//获取下一页
.hasMore()//是否还有更多
```
请求返回列表实例

```java
  new RequestPagerBuilder(getActivity(), this).api("Z002004")  .param("class_id", id) .setParse("list", ListItemArticle.class) .requestIndex();
```

自定义解析列表实例

```java
  new RequestPagerBuilder(getActivity(), this).api("Z002004")  .param("class_id", id)  .setParse(new RequestPagerParse(){
                        @Override
                       public ArrayList<Object> parse(JSONObject obj) {
                            JSONArray list = obj.optJSONArray("list");
                            return ParseUtil.parseListObject(null, list, ListItemActicleModel.class);
                         }
                    }) .requestIndex();
```

6、上传文件

```java
.api(String api)//配置api名字
.param(String key, Object value)//配置入参
.clean()//清除文件队列
.file(File file)//添加上传文件
.setParse(String key, Class<?> clazz)//解析model
.setParse(RequestParse parse)//自定义解析model
.setRequestFinish(RequestFinish requestFinish)//自定义请求成功调用方法
.ok(int resid)//请求成功提示文字 默认无
.error(int resid)//请求失败提示文字 默认提示出错信息
.setRequestHttpException(RequestHttpException requestHttpException）//自定义请求交互异常
.requestIndex()//发起请求
```

自定义解析上传文件实例

```java
 new RequestFileBuilder(activity).api("Z014006").param("file_count", 1).file(file)
                        .setParse(new RequestFileBuilder.RequestParse() {
                            @Override
                            public Object parse(JSONObject obj) {
                                return obj.optString("url");
                            }
                        }).requestIndex();
 ```
