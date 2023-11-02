-------------------------------------------------XMLCODE------------------------------------------------------------





<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <EditText
        android:id="@+id/editTextNumber1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Number 1" />

    <EditText
        android:id="@+id/editTextNumber2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Number 2" />

    <TextView
        android:id="@+id/textViewResult"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Result: "
        android:layout_gravity="center"
        android:layout_marginTop="16dp" />

    <Button
        android:id="@+id/buttonAdd"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="+"
        android:layout_gravity="center"
        android:layout_marginTop="20dp"/>

    <Button
        android:id="@+id/buttonSubtract"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="-"
        android:layout_gravity="center" />

    <Button
        android:id="@+id/buttonMultiply"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="*"
        android:layout_gravity="center" />

    <Button
        android:id="@+id/buttonDivide"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="/"
        android:layout_gravity="center" />

    <Button
        android:id="@+id/buttonClear"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Clear"
        android:layout_gravity="center" />



</LinearLayout>



------------------------------------------------MAINACTIVITY-------------------------------------------------------




package com.example.calculator;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private EditText editTextNumber1;
    private EditText editTextNumber2;
    private Button buttonAdd;
    private Button buttonSubtract;
    private Button buttonMultiply;
    private Button buttonDivide;
    private Button buttonClear;
    private TextView textViewResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextNumber1 = findViewById(R.id.editTextNumber1);
        editTextNumber2 = findViewById(R.id.editTextNumber2);
        buttonAdd = findViewById(R.id.buttonAdd);
        buttonSubtract = findViewById(R.id.buttonSubtract);
        buttonMultiply = findViewById(R.id.buttonMultiply);
        buttonDivide = findViewById(R.id.buttonDivide);
        buttonClear = findViewById(R.id.buttonClear);
        textViewResult = findViewById(R.id.textViewResult);

        buttonAdd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate("+");
            }
        });

        buttonSubtract.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate("-");
            }
        });

        buttonMultiply.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate("*");
            }
        });

        buttonDivide.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate("/");
            }
        });

        buttonClear.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                clearInputFields();
            }
        });
    }

    private void calculate(String operation) {
        String num1 = editTextNumber1.getText().toString();
        String num2 = editTextNumber2.getText().toString();

        if (!num1.isEmpty() && !num2.isEmpty()) {
            double result = 0;
            double number1 = Double.parseDouble(num1);
            double number2 = Double.parseDouble(num2);

            switch (operation) {
                case "+":
                    result = number1 + number2;
                    break;
                case "-":
                    result = number1 - number2;
                    break;
                case "*":
                    result = number1 * number2;
                    break;
                case "/":
                    if (number2 != 0) {
                        result = number1 / number2;
                    } else {
                        textViewResult.setText("Division by zero is not allowed");
                        return;
                    }
                    break;
            }

            textViewResult.setText("Result: " + result);
        } else {
            textViewResult.setText("Please enter two numbers");
        }
    }

    private void clearInputFields() {
        editTextNumber1.getText().clear();
        editTextNumber2.getText().clear();
        textViewResult.setText("Result: ");
    }
}
