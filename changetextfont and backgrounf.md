-------------------------------------------XMLCODE------------------------------------------------------------------





<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/helloText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!"
        android:layout_gravity="center"
        android:layout_margin="20dp"/>

    <Button
        android:id="@+id/changeButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Change Style"
        android:layout_gravity="center"
      
        />

</LinearLayout>

---------------------------------------------------MAINACTIVITY-----------------------------------------------------

package com.example.change;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import java.util.Random;

public class MainActivity extends AppCompatActivity {

    private TextView helloText;
    private Button changeButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        helloText = findViewById(R.id.helloText);
        changeButton = findViewById(R.id.changeButton);

        changeButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // Generate random colors for the background and text
                Random random = new Random();
                int backgroundColor = 0xff000000 | random.nextInt(0x00ffffff);
                int textColor = 0xff000000 | random.nextInt(0x00ffffff);

                // Set the background and text color
                helloText.setBackgroundColor(backgroundColor);
                helloText.setTextColor(textColor);

                // Change the font size randomly
                float fontSize = random.nextInt(30) + 20; // Font size between 20 and 50
                helloText.setTextSize(fontSize);
            }
        });
    }
}
