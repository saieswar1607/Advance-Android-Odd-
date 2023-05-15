# Ex.No:2 Create a simple application client and server service using AIDL interface in android studio.


## AIM:

To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as CSAIDL and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file(client/server).

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the client/server services using AIDL”.
Developed by: Sai Eswar Kandukuri
Registeration Number : 212221240020
*/
```

### MainActivity.java
```
package com.example.aidl;

//import androidx.appcompat.app.AppCompatActivity; 

import android.app.AppComponentFactory;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppComponentActivity implements View.OnClickListener {
    EditText edtnum1,edtnum2;
    Button btnMul;
    TextView textans;
    MultiplyInterface myInterface;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        edtnum1 = findViewById(R.id.edtnum1);
        edtnum2 = findViewById(R.id.edtnum2);
        btnMul = findViewById(R.id.btnMul);
        textans = findViewById(R.id.txtans);
        btnMul.setOnClickListener(MainActivity.this);
        Intent multiplyServie = new Intent(MainActivity.this,MultiplicationService.class);
        bindService(multiplyServie,myServiceConnection, Context.BIND_AUTO_CREATE);

    }
    ServiceConnection myServiceConnection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName name, IBinder iBinder) {
            myInterface = MultiplyInterface.Stub.asInterface(iBinder);

        }

        @Override
        public void onServiceDisconnected(ComponentName name) {

        }
    };

    @Override
    public void onClick(View v) {
        int firstNumber = Integer.parseInt(edtnum1.getText().toString());
        int secondNumber = Integer.parseInt(edtnum2.getText().toString());
        try{
            int result = myInterface.multiplyTwoValuesTogether(firstNumber,secondNumber);
            textans.setText(result+ "");

        }catch (RemoteException e){
            e.printStackTrace();
        }
//        int result = myInterface.multiplyTwoValuesTogether(firstNumber,secondNumber);
    }
}
```

### MultiplicationService.java
```
package com.example.aidl;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.os.RemoteException;

public class MultiplicationService extends Service {
    public MultiplicationService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        return myBinder;
    }
    MultiplyInterface.Stub myBinder = new MultiplyInterface.Stub() {
        @Override
        public int multiplyTwoValuesTogether(int firstNumber, int secondNumber) throws RemoteException {
            return firstNumber * secondNumber;
        }
    };
}
```

### MultiplyInterface.aidl
```
// MultiplyInterface.aidl
package com.example.aidl;

// Declare any non-default types here with import statements

interface MultiplyInterface {
  int multiplyTwoValuesTogether(int firstNumber, int secondNumber);
}
```

### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
<EditText
    android:id="@+id/edtnum1"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="100dp"
    android:layout_width="250dp"
    android:layout_height="50dp"

    android:hint="num1"/>

    <EditText
        android:id="@+id/edtnum2"
        android:layout_width="250dp"
        android:layout_height="50dp"
        android:layout_centerHorizontal="true"
        android:hint="num2"
        android:layout_below="@+id/edtnum1"/>
    <Button
        android:id="@+id/btnMul"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/edtnum2"
        android:layout_centerHorizontal="true"
        android:text="Multiply"
        android:layout_marginTop="10dp"/>
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/txtans"
        android:layout_below="@+id/btnMul"
        android:layout_marginTop="20dp"
        android:layout_centerHorizontal="true"/>


</RelativeLayout>
```

## OUTPUT

<img width="356" alt="out1" src="https://github.com/saieswar1607/Advance-Android-Odd-/assets/93427011/19dacede-e5fb-4711-ba15-04bac4735c27">

<img width="355" alt="out2" src="https://github.com/saieswar1607/Advance-Android-Odd-/assets/93427011/46382b00-468a-4867-b51b-caf56389ea7e">


## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.
