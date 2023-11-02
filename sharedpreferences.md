----------------------------------------MAINXML---------------------------------------------------------------------




<!-- res/layout/activity_main.xml -->
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/editTextUsername"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your username" />

    <Button
        android:id="@+id/buttonSave"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Save Username" />

    <TextView
        android:id="@+id/textViewSavedUsername"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Saved Username: " />

</LinearLayout>


-----------------------MAINACTIVITY---------------------------------------------------------------------


package com.example.sharedpreference;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private EditText usernameEditText;
    private Button saveButton;
    private TextView savedUsernameTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        usernameEditText = findViewById(R.id.editTextUsername);
        saveButton = findViewById(R.id.buttonSave);
        savedUsernameTextView = findViewById(R.id.textViewSavedUsername);

        // Retrieve and display the username (if it exists) when the activity starts
        String savedUsername = MySharedPreferences.getUsername(this);
        if (savedUsername != null) {
            usernameEditText.setText(savedUsername);
            savedUsernameTextView.setText("Saved Username: " + savedUsername);
        }

        saveButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Save the username when the button is clicked
                String username = usernameEditText.getText().toString();
                MySharedPreferences.saveUsername(MainActivity.this, username);
                savedUsernameTextView.setText("Saved Username: " + username);
            }
        });
    }
}





------------------------------------SHAREDPREFERENCE>JAVA  crete it by creating a newclass--------------------------




package com.example.sharedpreference;

import android.content.Context;
import android.content.SharedPreferences;

public class MySharedPreferences {
    private static final String PREF_NAME = "MyAppPreferences";
    private static final String KEY_USERNAME = "username";

    public static void saveUsername(Context context, String username) {
        SharedPreferences preferences = context.getSharedPreferences(PREF_NAME, Context.MODE_PRIVATE);
        SharedPreferences.Editor editor = preferences.edit();
        editor.putString(KEY_USERNAME, username);
        editor.apply();
    }

    public static String getUsername(Context context) {
        SharedPreferences preferences = context.getSharedPreferences(PREF_NAME, Context.MODE_PRIVATE);
        return preferences.getString(KEY_USERNAME, null);
    }
}
