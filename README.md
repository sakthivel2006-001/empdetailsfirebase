
# Ex.No:1 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by:SAKTHIVEL S
Registeration Number :212223220090
*/
```
```
/*
Main Activity in Java Folder
package com.example.ex_01_realtimedatabase;

import android.os.Bundle;
import android.widget.*;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.*;

import java.util.*;

public class MainActivity extends AppCompatActivity {

    EditText etName, etAge, etSalary;
    Button btnAdd, btnUpdate, btnDelete;
    ListView listView;

    DatabaseReference dbRef;

    ArrayList<String> items = new ArrayList<>();
    ArrayList<String> keys = new ArrayList<>();

    ArrayAdapter<String> adapter;

    String selectedKey = null;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        // Initialize views
        etName = findViewById(R.id.etName);
        etAge = findViewById(R.id.etAge);
        etSalary = findViewById(R.id.etSalary);

        btnAdd = findViewById(R.id.btnAdd);
        btnUpdate = findViewById(R.id.btnUpdate);
        btnDelete = findViewById(R.id.btnDelete);

        listView = findViewById(R.id.listView);

        // Firebase reference
        dbRef = FirebaseDatabase.getInstance().getReference("Employees");

        // ListView adapter
        adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                items
        );

        listView.setAdapter(adapter);

        // Read data from Firebase
        dbRef.addValueEventListener(new ValueEventListener() {

            @Override
            public void onDataChange(DataSnapshot snapshot) {

                items.clear();
                keys.clear();

                for (DataSnapshot d : snapshot.getChildren()) {

                    Emp e = d.getValue(Emp.class);

                    if (e != null) {
                        items.add(e.name + " | " + e.age + " | " + e.salary);
                        keys.add(d.getKey());
                    }
                }

                adapter.notifyDataSetChanged();
            }

            @Override
            public void onCancelled(DatabaseError error) {
            }
        });

        // Add employee
        btnAdd.setOnClickListener(v -> {

            Emp e = new Emp(
                    etName.getText().toString(),
                    etAge.getText().toString(),
                    etSalary.getText().toString()
            );

            dbRef.push().setValue(e);

            clearFields();
        });

        // Update employee
        btnUpdate.setOnClickListener(v -> {

            if (selectedKey != null) {

                Emp e = new Emp(
                        etName.getText().toString(),
                        etAge.getText().toString(),
                        etSalary.getText().toString()
                );

                dbRef.child(selectedKey).setValue(e);

                clearFields();

            } else {

                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Delete employee
        btnDelete.setOnClickListener(v -> {

            if (selectedKey != null) {

                dbRef.child(selectedKey).removeValue();

                clearFields();

            } else {

                Toast.makeText(
                        this,
                        "Select an item first",
                        Toast.LENGTH_SHORT
                ).show();
            }
        });

        // Select employee from ListView
        listView.setOnItemClickListener((p, v, pos, id) -> {

            selectedKey = keys.get(pos);

            dbRef.child(selectedKey).get().addOnSuccessListener(d -> {

                Emp e = d.getValue(Emp.class);

                if (e != null) {

                    etName.setText(e.name);
                    etAge.setText(e.age);
                    etSalary.setText(e.salary);
                }
            });
        });
    }

    // Clear input fields
    private void clearFields() {

        etName.setText("");
        etAge.setText("");
        etSalary.setText("");

        selectedKey = null;
    }
}
*/
```
```
/*
Layout part “Design” “activity_mail.xml”
```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <!-- Name -->
    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="55dp"
        android:hint="Name" />

    <!-- Age -->
    <EditText
        android:id="@+id/etAge"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Age"
        android:inputType="number" />

    <!-- Salary -->
    <EditText
        android:id="@+id/etSalary"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Salary"
        android:inputType="number" />

    <!-- Buttons -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnAdd"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Add" />

        <Button
            android:id="@+id/btnUpdate"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Update" />

        <Button
            android:id="@+id/btnDelete"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Delete" />

    </LinearLayout>

    <!-- ListView -->
    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
*/
```

## OUTPUT
<img width="1920" height="1080" alt="Screenshot 2026-11-02 082229" src="https://github.com/user-attachments/assets/f74138e6-61dc-4a34-a66b-210a179dee22" />
<img width="1885" height="1066" alt="Screenshot 2026-11-02 083639" src="https://github.com/user-attachments/assets/a94fc421-8174-48e9-88aa-09df41d4a421" />
<img width="1920" height="1080" alt="Screenshot 2026-11-02 083556" src="https://github.com/user-attachments/assets/33700100-5519-4e0e-aa03-639ffbff6ebc" />



## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
