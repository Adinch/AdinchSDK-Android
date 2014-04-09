AdinchSDK-Android
=================

The integration of the Adinch advertising library.
-----------------

To integrate Adinch SDK into your application you need to make next steps:


1) Add please to project to the folder libs adinch_sdk.jar, to the folder res/values file adinch_attrs.xml

To add an advertisement must be placed on activity AdinchLayout300x250 for banners size 300x250 or AdinchLayout320x50 for banners  size of 320x50

2) You can add AdinchLayout in the code:

    adinchLayout = new AdinchLayout320x50(this, "<YOUR_ADINCH_KEY>"); // or  new AdinchLayout300x250(this, "<YOUR_ADINCH_KEY>");
    RelativeLayout.LayoutParams layoutParams = new RelativeLayout.LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
    mainLayout.addView(adinchLayout, layoutParams);
    mainLayout.invalidate();
    
or register to xml file activity:

    <com.adinch.ads.AdinchLayout300x250 
        xmlns:ads="http://schemas.android.com/apk/res-auto"
        android:id="@+id/adsLoyout"
        android:layout_width="300dp"
        android:layout_height="250dp"     
        ads:keyAdinch="<YOUR_ADINCH_KEY>" />
or

    <com.adinch.ads.AdinchLayout320x50 
        xmlns:ads="http://schemas.android.com/apk/res-auto"
        android:id="@+id/adsLoyout"
        android:layout_width="320dp"
        android:layout_height="50dp"      
        ads:keyAdinch="<YOUR_ADINCH_KEY>" />

in the initialization method activity register:

    AdinchLayout adinchLayout = (AdinchLayout)findViewById(R.id.adsLayout);
    
3)You can add callback to AdinchLayout

    // The parameter must send an application context
    adinchLayout.setAdsCallback(new IAdsAdinchCallback() {
        @Override
        public void onAdsLoadingOk() {
        }
        @Override
        public void onAdsLoadingError(int code, String msg) {
            
        }
    });
4)necessarily add to the Android Manifest:
  Add the following mandatory permissions to AndroidManifest.xml

    <uses-permission android:name="android.permission.INTERNET" />
  And the following optional permissions

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  
5) Add google-play-services to your project
    
   

This part of our functionality meets the requirements of <a href=http://www.apache.org/licenses/LICENSE-2.0.html>Apache License, Version 2.0</a>. All copyrights respected.

