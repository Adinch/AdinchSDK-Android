AdinchSDK-Android
=================

The integration of the Adinch advertising library
---------------------

To integrate Adinch SDK into your application you need to make next steps:

1) You must declare the interface  AdinchInterface, such as
    extends Activity implements AdinchInterface{
      ...
    @Override
      public void adinchGeneric() {}
      }
2) After that, initialize the library according to its Adinch documentation:

    AdinchManager.setConfigExpireTimeout(1000 * 15);
    AdinchTargeting.setAge(0);
    AdinchTargeting.setGender(AdinchTargeting.Gender.MALE);
    AdinchTargeting.setKeywords("<YOUR_KEYWORDS>");
    AdinchTargeting.setPostalCode("<YOUR_POSTAL_CODE");
    AdinchTargeting.setTestMode(true);
3) Вы можете добавить AdinchLayout в коде:

    adinchLayout = new AdinchLayout(this, "<YOUR_ADINCH_KEY>");
    RelativeLayout.LayoutParams layoutParams = new RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
    int diWidth = 320;
    int diHeight = 52;
    float density = (float) getResources().getDisplayMetrics().density;

    /**You must specify the interface through which Adinch will interact with the application*/

    adinchLayout.setAdinchInterface(this); // parameter specifies the implementation of the interface AdinchInterface
    adinchLayout.setMaxWidth((int) (diWidth * density));
    adinchLayout.setMaxHeight((int) (diHeight * density));
    layoutParams.addRule(RelativeLayout.CENTER_HORIZONTAL);
    RelativeLayout mainLayout = (RelativeLayout) findViewById(R.id.ads_layout);
    mainLayout.addView(adinchLayout, layoutParams);
    mainLayout.invalidate();
    
или прописать в xml файле activity:
    <com.adinch.mediation.AdinchLayout
        android:id="@+id/adsLoyout"        
        android:layout_width="320dp"
        android:layout_height="50dp"
        android:layout_gravity="center_vertical"/>

в методе инициализации activity прописать:
    AdinchLayout adinchLayout = (AdinchLayout)findViewById(R.id.adsLayout);

4)обязательно добавить в Android Manifest:
  - ключ adinch 
    <meta-data android:value="<YOUR_ADINCH_KEY>" android:name="ADINCH_KEY" />
    
  - permissions:

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  - необходимые activity для подключаемых реклам:

    <activity
            android:name="com.google.ads.AdActivity"
            android:configChanges="orientation|keyboard|keyboardHidden|screenLayout|uiMode|screenSize|smallestScreenSize" />
        <!-- MdotM integration -->
        <activity android:name="com.mdotm.android.ads.MdotmLandingPage"
                  android:label="@string/app_name" >
            <intent-filter>
                <category android:name="android.intent.category.BROWSABLE" />
            </intent-filter>
        </activity>
        <!-- Millennial integration -->
        <activity android:name="com.millennialmedia.android.MMAdViewOverlayActivity"
                  android:theme="@android:style/Theme.NoTitleBar.Fullscreen"
                  android:configChanges="orientation|keyboard|keyboardHidden" />
        <activity android:name="com.millennialmedia.android.VideoPlayer"
                  android:theme="@android:style/Theme.NoTitleBar.Fullscreen"
                  android:configChanges="keyboardHidden|orientation|keyboard" />
        <!-- InMobi integration -->
        <activity android:name="com.inmobi.androidsdk.IMBrowserActivity"
                  android:configChanges="keyboardHidden|orientation|keyboard" />
  