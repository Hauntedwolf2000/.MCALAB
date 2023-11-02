activity_main.xml

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
   android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
   android:paddingRight="@dimen/activity_horizontal_margin"
   android:paddingTop="@dimen/activity_vertical_margin"
   android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">

   <TextView
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:textAppearance="?android:attr/textAppearanceMedium"
       android:text="If you click on Explicit example we will navigate to second activity within App and if you click on Implicit example AbhiAndroid Homepage will open in Browser"
       android:id="@+id/textView2"
       android:clickable="false"
       android:layout_alignParentTop="true"
       android:layout_alignParentStart="true"
       android:layout_marginTop="42dp"
       android:background="#3e7d02"
       android:textColor="#ffffff" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Explicit Intent Example"
       android:id="@+id/explicit_Intent"
       android:layout_alignParentTop="true"
       android:layout_centerHorizontal="true"
       android:layout_marginTop="147dp" />

   <Button
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Implicit Intent Example"
       android:id="@+id/implicit_Intent"
       android:layout_centerVertical="true"
       android:layout_centerHorizontal="true" />

</RelativeLayout>


Second_activity.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
   android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
   android:paddingRight="@dimen/activity_horizontal_margin"
   android:paddingTop="@dimen/activity_vertical_margin"
   android:paddingBottom="@dimen/activity_vertical_margin"
   android:background="#CCEEAA"
   tools:context="com.example.intents.SecondActivity">

   <TextView
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:textAppearance="?android:attr/textAppearanceLarge"
       android:text="This is Second Activity"
       android:id="@+id/textView"
       android:layout_centerVertical="true"
       android:layout_centerHorizontal="true" />
</RelativeLayout>

Mainactivity.java

package com.example.in;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {


   Button explicit_btn, implicit_btn;
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);


       explicit_btn = (Button)findViewById(R.id.explicit_Intent);
       implicit_btn = (Button) findViewById(R.id.implicit_Intent);

       //implement Onclick event for Explicit Intent

       explicit_btn.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {

               Intent intent = new  Intent(getBaseContext(), com.example.in.SecondActivity.class);
               startActivity(intent);


           }
       });

       //implement onClick event for Implicit Intent

       implicit_btn.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {

               Intent intent = new Intent(Intent.ACTION_VIEW);
               intent.setData(Uri.parse("https://www.abhiandroid.com"));
               startActivity(intent);
           }
       });


   }
}

Secondactivity.java
package com.example.in;

import android.os.Bundle;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class SecondActivity extends AppCompatActivity {

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_second);

       Toast.makeText(getApplicationContext(), "We are moved to second Activity",Toast.LENGTH_LONG).show();
   }
}