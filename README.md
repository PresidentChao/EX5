# EX5
## 1.设计思路
### （1）先写一个浏览器，再写一个输入网址，点击访问，选择浏览器并调用写好的浏览器
### （2）效果展示
![linearlayout](https://github.com/PresidentChao/EX5/blob/master/1.png)
![linearlayout](https://github.com/PresidentChao/EX5/blob/master/2.png)
![linearlayout](https://github.com/PresidentChao/EX5/blob/master/3.png)
## 2.主要代码
### （1）浏览器
#### MyWebView
#####
    public class MyWebView extends AppCompatActivity {

    private WebView webView;
    private String Url;


    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initView();
        setWebView();
    }

    private void initView() {
        webView= (WebView) findViewById(R.id.webView);
        Uri url=getIntent().getData();
        if(url==null){
            Url="https://www.baidu.com";
        }
        else {
            Url=url.toString();
        }
        Log.e("asd ",Url);
    }


    private void setWebView() {
        WebSettings webSettings=webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setSupportZoom(true);

        webView.loadUrl(Url);
        webView.setWebViewClient(new WebViewClient(){

            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                webView.loadUrl(Url);
                return true;
            }
        });
    }
#### AndroidManifest.xml
##### 
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.lenovo.ex5_webview">


    <uses-permission  android:name="android.permission.INTERNET"/>
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MyWebView">
            <intent-filter>

                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

            <intent-filter>

                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE"/>

                <data android:scheme="http"/>
                <data android:scheme="https"/>
            </intent-filter>

        </activity>
    </application>

</manifest>

### （2）输入网址，调用浏览器访问
#### activity_main.xml
##### 
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="com.example.lenovo.ex5.MainActivity">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        >
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp"
            android:hint="输入网址"
            android:layout_weight="1"
            android:id="@+id/et_url"
            />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="访问"
            android:id="@+id/btn_go"
            />
    </LinearLayout>


    <WebView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/my_webView"
        >

    </WebView>

</LinearLayout>
#### MainActivity
