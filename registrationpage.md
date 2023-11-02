-----------------------------------------XMLCODE----------------------------------------------------------------



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

   <EditText
       android:id="@+id/usernameEditText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Username"
       />

   <EditText
       android:id="@+id/emailEditText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Email"
       />

   <EditText
       android:id="@+id/passwordEditText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Password"
       android:inputType="textPassword"
       />

   <EditText
       android:id="@+id/verifyPasswordEditText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Verify Password"
       android:inputType="textPassword"
       />

   <CheckBox
       android:id="@+id/termsCheckBox"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="I agree to the Terms and Conditions"
       />

   <RadioGroup
       android:id="@+id/roleRadioGroup"
       android:layout_width="match_parent"
       android:layout_height="wrap_content">

      <RadioButton
          android:id="@+id/adminRadioButton"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Admin"
          />

      <RadioButton
          android:id="@+id/userRadioButton"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="User"
          />
   </RadioGroup>

   <Button
       android:id="@+id/registerButton"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Register"
       android:layout_gravity="center"
       />

</LinearLayout>



---------------------------------------------MAINACTIVITY-----------------------------------------------------------






package com.example.registrationpage;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class RegistrationActivity extends AppCompatActivity {

    EditText usernameEditText, emailEditText, passwordEditText, verifyPasswordEditText;
    CheckBox termsCheckBox;
    RadioGroup roleRadioGroup;
    Button registerButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        usernameEditText = findViewById(R.id.usernameEditText);
        emailEditText = findViewById(R.id.emailEditText);
        passwordEditText = findViewById(R.id.passwordEditText);
        verifyPasswordEditText = findViewById(R.id.verifyPasswordEditText);
        termsCheckBox = findViewById(R.id.termsCheckBox);
        roleRadioGroup = findViewById(R.id.roleRadioGroup);
        registerButton = findViewById(R.id.registerButton);

        registerButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String username = usernameEditText.getText().toString();
                String email = emailEditText.getText().toString();
                String password = passwordEditText.getText().toString();
                String verifyPassword = verifyPasswordEditText.getText().toString();
                boolean termsAccepted = termsCheckBox.isChecked();
                String role = getSelectedRole();

                if (username.isEmpty() || email.isEmpty() || password.isEmpty() || verifyPassword.isEmpty() || role == null) {
                    showToast("Please fill in all fields.");
                } else if (!password.equals(verifyPassword)) {
                    showToast("Passwords do not match.");
                } else if (!termsAccepted) {
                    showToast("Please accept the Terms and Conditions.");
                } else {
                    // Registration successful, handle the registration logic here
                    showToast("Registration successful. Role: " + role);
                }
            }
        });
    }

    private String getSelectedRole() {
        int selectedRadioButtonId = roleRadioGroup.getCheckedRadioButtonId();

        if (selectedRadioButtonId == -1) {
            return null;
        }

        RadioButton selectedRadioButton = findViewById(selectedRadioButtonId);
        return selectedRadioButton.getText().toString();
    }

    private void showToast(String message) {
        Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
    }
}

