AdinchSDK-Android
=================

The integration of the Adinch advertising library.
-----------------

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
3) You can add AdinchLayout in the code:

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
or register to xml file activity:

    <com.adinch.mediation.AdinchLayout
        android:id="@+id/adsLoyout"        
        android:layout_width="320dp"
        android:layout_height="50dp"
        android:layout_gravity="center_vertical"/>

in the initialization method activity register:

    AdinchLayout adinchLayout = (AdinchLayout)findViewById(R.id.adsLayout);
4)necessarily add to the Android Manifest:
  adinch key 
  
    <meta-data android:value="<YOUR_ADINCH_KEY>" android:name="ADINCH_KEY" />
  Add the following mandatory permissions to AndroidManifest.xml

    <uses-permission android:name="android.permission.INTERNET" />
  And the following optional permissions

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  required activity for connected advertising:
  
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
The integration of the Adinch advertising library into AdWhirl
-----------------
Here are the steps to integrate an advertising network Adinch into  AdWhirl by a mechanism CustomEvents.

1) In the interface of  AdWhirl advertising managing platform you need to push the button “+Add Custom Event”  at the page “Ad Networl settings” and specify the name of the method that will initialize the Adinch library.

2) You must declare the interface  AdWhirlInterface, such as

    extends Activity implements AdWhirlInterface{
    @Override
    public void adWhirlGeneric() {
        Log.v(TAG, "adWhirlGeneric()");
    }}
3) After that, initialize the library according to its AdWhirl documentation:

    AdWhirlManager.setConfigExpireTimeout(1000 * 15);
    AdWhirlTargeting.setAge(0);
    AdWhirlTargeting.setGender(AdWhirlTargeting.Gender.MALE);
    AdWhirlTargeting.setKeywords("<YOUR_KEYWORDS>");
    AdWhirlTargeting.setPostalCode("<YOUR_POSTAL_CODE");
    AdWhirlTargeting.setTestMode(true);
    adWhirlLayout = new AdWhirlLayout(this, "<YOUR_ADWHIRL_KEY>");
    RelativeLayout.LayoutParams layoutParams = new 	RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
    int diWidth = 320;
    int diHeight = 52;
    float density = (float) getResources().getDisplayMetrics().density;
    /**You must specify the interface through which AdWhirl will interact with the application*/
    adWhirlLayout.setAdWhirlInterface(this); // parameter specifies the implementation of the interface AdWhirlInterface
    adWhirlLayout.setMaxWidth((int) (diWidth * density));
    adWhirlLayout.setMaxHeight((int) (diHeight * density));
    layoutParams.addRule(RelativeLayout.CENTER_HORIZONTAL);
    RelativeLayout mainLayout = (RelativeLayout) findViewById(R.id.ads_layout);
    mainLayout.addView(adWhirlLayout, layoutParams);
    mainLayout.invalidate();

    // The parameter must send an application context
    ad = new AdsView(this, AdsView.MANUAL);
    ad.setCallback(new IAdinchCallback() {
        @Override
        public void onAdsLoadingOk() {
        }
        @Override
        public void onAdsLoadingError(int code, String msg) {
            adWhirlLayout.rollover();
        }
    });
    /**
    Connecting the library to AdWhirl
    */
    adWhirlLayout.handler.post(new AdWhirlLayout.ViewAdRunnable(adWhirlLayout, ad));
4) You must implement a method that matches the naming
name of claim 1, and initialize it to run the library Adinch:

    public void adinchEvent(){
        /**Initialization of the Adinch library within the AdWhirl*/
        adWhirlLayout.adWhirlManager.resetRollover();
        ad.show();
        adWhirlLayout.handler.post(new AdWhirlLayout.ViewAdRunnable(adWhirlLayout, ad));
        adWhirlLayout.rotateThreadedDelayed();
    }
Remember to specify definition:

   Add the following mandatory permissions to AndroidManifest.xml

    <uses-permission android:name="android.permission.INTERNET" />
  And the following optional permissions

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
in AndroidManifest.xml


This part of our functionality meets the requirements of <a href=http://www.apache.org/licenses/LICENSE-2.0.html>Apache License, Version 2.0</a>. All copyrights respected.

The development is based on <a href=http://code.google.com/p/adwhirl/>the source codes</a> of <a href=https://www.adwhirl.com/>AdWhirl.</a>
