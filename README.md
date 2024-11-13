
# Codingan Activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Simple Calculator"
        android:layout_gravity="center"
        android:textStyle="bold"
        android:layout_marginTop="50dp"
        android:textSize="30sp"/>

    <EditText
        android:id="@+id/number1"
        android:hint="Enter number"
        android:layout_marginTop="30dp"
        android:inputType="number"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/number2"
        android:hint="Enter number"
        android:layout_marginTop="10dp"
        android:inputType="number"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <LinearLayout
        android:orientation="horizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:gravity="center">

        <Button
            android:id="@+id/btn_add"
            android:text="+"
            android:textSize="30sp"
            android:layout_marginEnd="5dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btn_sub"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginEnd="5dp"
            android:text="-"
            android:textSize="30sp" />

        <Button
            android:id="@+id/btn_mul"
            android:text="x"
            android:textSize="30sp"
            android:layout_marginEnd="5dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btn_div"
            android:text="/"
            android:textSize="30sp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>
    </LinearLayout>

    <TextView
        android:id="@+id/answer"
        android:layout_gravity="center"
        android:layout_marginTop="30dp"
        android:textStyle="bold"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</LinearLayout>


# Codingan MainActivity.java
package com.example.simple_calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText number1, number2;
    private Button btnAdd, btnSub, btnMul, btnDiv;
    private TextView answer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        number1 = findViewById(R.id.number1);
        number2 = findViewById(R.id.number2);
        btnAdd = findViewById(R.id.btn_add);
        btnSub = findViewById(R.id.btn_sub);
        btnMul = findViewById(R.id.btn_mul);
        btnDiv = findViewById(R.id.btn_div);
        answer = findViewById(R.id.answer);

        btnAdd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate('+');
            }
        });

        btnSub.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate('-');
            }
        });

        btnMul.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate('*');
            }
        });

        btnDiv.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculate('/');
            }
        });
    }

    private void calculate(char operator) {
        String num1String = number1.getText().toString();
        String num2String = number2.getText().toString();

        if (num1String.isEmpty() || num2String.isEmpty()) {
            Toast.makeText(this, "Please enter both numbers", Toast.LENGTH_SHORT).show();
            return;
        }

        double num1 = Double.parseDouble(num1String);
        double num2 = Double.parseDouble(num2String);
        double answerValue = 0;

        switch (operator) {
            case '+':
                answerValue = num1 + num2;
                break;
            case '-':
                answerValue = num1 - num2;
                break;
            case '*':
                answerValue = num1 * num2;
                break;
            case '/':
                if (num2 != 0) {
                    answerValue = num1 / num2;
                } else {
                    Toast.makeText(this, "Cannot divide by zero", Toast.LENGTH_SHORT).show();
                    return;
                }
                break;
        }

        answer.setText("Answer: " + answerValue);
    }
}



