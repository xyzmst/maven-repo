# How to use

Simply add the repository to your build.gradle file:
```
repositories {
    maven {
        url 'https://raw.githubusercontent.com/xyzmst/maven-repo/master/'
    }
    mavenCentral()
}
```
And you can use the artifacts like this:
```
dependencies {
    compile 'org.xyzmst:wxsdk:1.0'
    compile 'org.xyzmst:alisdk:1.0'
    compile 'org.xyzmst:ViewPagerIndicator:2.4.1'
    compile 'org.xyzmst:DatePicker:2.2.0'
    compile 'org.xyzmst:materialfilepicker:1.0.8'
    compile 'org.xyzmst:pay:1.0.5'
    compile 'de.greenrobot:eventbus:2.2.1'
    compile 'org.xyzmst:sprinkles:2.1.12'
    compile 'org.xyzmst:android-gif-drawable:1.1.17'
}
```

### 说明
- pay: 支付集成
  1.0.2 修复了 因java中package是关键字，而订单详情的返回值为package ，"Sign=WXPay"无法添加到订单详情导致无法打开微信的问题
  1.0.5 删除了 包内的 WXPayEntryActivity
  使用时需要配置，有问题参考 http://xyzmst.top/2016/07/22/%E6%94%AF%E4%BB%98%E9%9B%86%E6%88%90/
  需要将当前应用的包下，加入wxapi包路径并实现WXPayEntryActivity类
使用时需要 再清单文件配置，否则不会回调，切记
```
<activity
            android:name=".wxapi.WXPayEntryActivity"
            android:exported="true"
            android:launchMode="singleTop"/>
```
粘出实现

``` java
public class WXPayEntryActivity extends Activity implements IWXAPIEventHandler {
    private static final String TAG = "WXPayEntryActivity";
    private IWXAPI api;

    public WXPayEntryActivity() {
    }

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        this.api = WXAPIFactory.createWXAPI(this, KeyLibs.weixin_appId);
        this.api.handleIntent(this.getIntent(), this);
    }

    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        this.setIntent(intent);
        this.api.handleIntent(intent, this);
    }

    public void onReq(BaseReq req) {
    }

    public void onResp(final BaseResp resp) {
        Log.d("WXPayEntryActivity", "onPayFinish, errCode = " + resp.errCode);
        if (resp.getType() == 5) {
            (new Thread() {
                public void run() {
                    PayMessageEvent event = new PayMessageEvent();
                    event.code = resp.errCode + "";
                    event.message = PayResultCode.getMessage(event.code);
                    event.type = PayType.WeixinPay;
                    EventBus.getDefault().post(event);
                }
            }).start();
            this.finish();
        }

    }
}
```

回调使用
``` java
 @Override
    public void onResume() {
        super.onResume();
        EventBus.getDefault().unregister(this);
        EventBus.getDefault().register(this);
    }
 @Override
    protected void onDestroy() {
        EventBus.getDefault().unregister(this);
        super.onDestroy();
    }

public void onEventMainThread(final PayMessageEvent event) {
        if (event != null) {
            if (event.type == PayType.AliPay) {
                if (event.code.equals(PayResultCode.ALI_SUCCESS)) {
                  
                } else {
                    
                }
            }
            if (event.type == PayType.WeixinPay) {
                if (event.code.equals(PayResultCode.WX_SUCCESS)) {
                    
                } else {
                    
                }
            }
        }

    }
```


- DatePicker ： 日期选择    
- materialfilepicker: 文件选择器
- sprinkles :数据库
- android-gif-drawable：gif
