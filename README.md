# Qr-Code-Reader-Sample-App
Qr Code reader sample application using ZXing 



##ZXing

Installation

Add the following dependency to your build.gradle file.

#compile 'me.dm7.barcodescanner:zxing:1.9.8'

#Simple Usage

#1.) Add camera permission to your AndroidManifest.xml file:

<uses-permission android:name="android.permission.CAMERA" />

#2.) Activity.java

``` public class MainActivity extends AppCompatActivity implements ZXingScannerView.ResultHandler{

    private ZXingScannerView scannerView;
    private TextView scannerText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        scannerView = new ZXingScannerView(this);
        scannerView.setAspectTolerance(0.1f);
        scannerView.setAutoFocus(true);

        scannerView = findViewById(R.id.scanner_view);
        scannerText = findViewById(R.id.qr_scanner_tex);

    }



    @Override
    public void onResume() {
        super.onResume();
        scannerView.setResultHandler(this); // Register ourselves as a handler for scan results.
        scannerView.startCamera();          // Start camera on resume
    }

    @Override
    public void onPause() {
        super.onPause();
        scannerView.stopCamera();           // Stop camera on pause
    }

    @Override
    public void handleResult(Result rawResult) {
        // Do something with the result here
        scannerText.setText(rawResult.getText().toString());

        // If you would like to resume scanning, call this method below:
        scannerView.resumeCameraPreview(this);
    }
}```


Activity.xml


```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical"
    >



    <me.dm7.barcodescanner.zxing.ZXingScannerView
        android:id="@+id/scanner_view"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="2"
        android:background="#000"
        >


    </me.dm7.barcodescanner.zxing.ZXingScannerView>



    <TextView
        android:id="@+id/qr_scanner_tex"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:text="Hello World!"
        android:gravity="center"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</LinearLayout>

```
