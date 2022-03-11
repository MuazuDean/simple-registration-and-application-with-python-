# simple-registration-and-application-with-python-
registration  form with python 



First, you will have to download & install the Android Development IDE (Android Studio or Eclipse). Android Studio is an open source development feel free to develop your things.

Here's the link for the Android Studio https://developer.android.com/studio/index.html.

Layout Design
We will now create the design for the application, first locate the layout file called activity_main.xml, this is the default name when create a new activity. Then write these codes inside your layout file.

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.razormist.simpleregistrationandloginapplication.MainActivity">
 
 
    <EditText
        android:id="@+id/et_username"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="65dp"
        android:ems="10"
        android:inputType="text"
        android:hint="Username"/>
 
 
    <EditText
        android:id="@+id/et_password"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="65dp"
        android:ems="10"
        android:layout_below="@+id/et_username"
        android:inputType="textPassword"
        android:hint="Password"/>
 
    <EditText
        android:id="@+id/et_cpassword"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="65dp"
        android:ems="10"
        android:layout_below="@+id/et_password"
        android:inputType="textPassword"
        android:hint="Confirm Password"/>
 
    <Button
        android:id="@+id/btn_register"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="65dp"
        android:ems="10"
        android:text="Register"
        android:layout_below="@+id/et_cpassword" />
 
    <Button
        android:id="@+id/btn_login"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:ems="10"
        android:text="Login"
        android:layout_alignParentBottom="true"/>
 
 
</RelativeLayout>

 
Then after that create a new empty activity called Login. It will also created a new java file called Login. Locate the new layout file called activity_login.xml and write these code inside the file.
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.razormist.simpleregistrationandloginapplication.Login">
 
    <EditText
        android:id="@+id/et_lusername"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="145dp"
        android:ems="10"
        android:inputType="text"
        android:hint="Username" />
 
    <EditText
        android:id="@+id/et_lpassword"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/et_lusername"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="50dp"
        android:ems="10"
        android:inputType="textPassword"
        android:hint="Password" />
 
    <Button
        android:id="@+id/btn_llogin"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/et_lpassword"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="50dp"
        android:ems="10"
        android:text="Login"/>
 
    <Button
        android:id="@+id/btn_lregister"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:ems="10"
        android:text="Register"/>
 
 
</RelativeLayout>
Android Manifest File
The Android Manifest file provides essential information about your app to the Android system in which the system must required before running the code. It describe the overall information about the application. It contains some libraries that needed to access the several method within the app.

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.razormist.simpleregistrationandloginapplication">
 
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".Login"
            android:configChanges="orientation"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name=".MainActivity"
            android:configChanges="orientation"
            android:label="@string/app_name"
            android:theme="@style/AppTheme">
            <intent-filter>
                <action android:name="com.razormist.simpleregistrationandloginapplication.Login" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
 
</manifest>

 
Creating The Database
This code contain the script for creating a database and a database connection. To create this first create a new java file called DatabaseHelper, open the newly created file then extend the class by adding SQLiteOpenHelper. After that write these block of codes inside the DatabaseHelper class.

 public static final String DATABASE_NAME = "login.db";
 
 
    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, 1);
    }
 
    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE user(ID INTEGER PRIMARY KEY AUTOINCREMENT, username TEXT, password TEXT)");
    }
 
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXIST user");
    }
 
    public boolean Insert(String username, String password){
        SQLiteDatabase sqLiteDatabase = this.getWritableDatabase();
        ContentValues contentValues = new ContentValues();
        contentValues.put("username", username);
        contentValues.put("password", password);
        long result = sqLiteDatabase.insert("user", null, contentValues);
        if(result == -1){
            return false;
        }else{
            return true;
        }
    }
 
    public Boolean CheckUsername(String username){
        SQLiteDatabase sqLiteDatabase = this.getWritableDatabase();
        Cursor cursor = sqLiteDatabase.rawQuery("SELECT * FROM user WHERE username=?", new String[]{username});
        if(cursor.getCount() > 0){
            return false;
        }else{
            return true;
        }
    }
 
    public Boolean CheckLogin(String username, String password){
        SQLiteDatabase sqLiteDatabase = this.getReadableDatabase();
        Cursor cursor = sqLiteDatabase.rawQuery("SELECT * FROM user WHERE username=? AND password=?", new String[]{username, password});
        if(cursor.getCount() > 0){
            return true;
        }else{
            return false;
        }
    }
Creating the Registration
This code contains the register function of the application. This will insert the data to the database by calling the DatabaseHelper when the button is clicked. To do that just write these block of codes inside the MainActivity class.

package com.razormist.simpleregistrationandloginapplication;
 
import android.content.Intent;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
 
public class MainActivity extends AppCompatActivity {
    DatabaseHelper databaseHelper;
 
    EditText et_username, et_password, et_cpassword;
    Button btn_register, btn_login;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        databaseHelper = new DatabaseHelper(this);
        et_username = (EditText)findViewById(R.id.et_username);
        et_password = (EditText)findViewById(R.id.et_password);
        et_cpassword = (EditText)findViewById(R.id.et_cpassword);
        btn_register = (Button)findViewById(R.id.btn_register);
        btn_login = (Button)findViewById(R.id.btn_login);
 
        btn_login.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, Login.class);
                startActivity(intent);
            }
        });
 
        btn_register.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String username = et_username.getText().toString();
                String password = et_password.getText().toString();
                String confirm_password = et_cpassword.getText().toString();
 
                if(username.equals("") || password.equals("") || confirm_password.equals("")){
                    Toast.makeText(getApplicationContext(), "Fields Required", Toast.LENGTH_SHORT).show();
                }else{
                    if(password.equals(confirm_password)){
                        Boolean checkusername = databaseHelper.CheckUsername(username);
                        if(checkusername == true){
                            Boolean insert = databaseHelper.Insert(username, password);
                            if(insert == true){
                                Toast.makeText(getApplicationContext(), "Registered", Toast.LENGTH_SHORT).show();
                                et_username.setText("");
                                et_password.setText("");
                                et_cpassword.setText("");
                            }
                        }else{
                            Toast.makeText(getApplicationContext(), "Username already taken", Toast.LENGTH_SHORT).show();
                        }
                    }else{
                        Toast.makeText(getApplicationContext(), "Password does not match", Toast.LENGTH_SHORT).show();
                    }
                }
            }
        });
    }
}
Creating the Login
This code contains the login function for the application. This code will read the entry field data then check the data if it exist in the DatabaseHelper class. To do that simply write these block of codes inside the Login class.

package com.razormist.simpleregistrationandloginapplication;
 
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
 
 
public class Login extends AppCompatActivity {
    Button btn_lregister, btn_llogin;
    EditText et_lusername, et_lpassword;
 
    DatabaseHelper databaseHelper;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
 
        databaseHelper = new DatabaseHelper(this);
 
        et_lusername = (EditText)findViewById(R.id.et_lusername);
        et_lpassword = (EditText)findViewById(R.id.et_lpassword);
 
        btn_llogin = (Button)findViewById(R.id.btn_llogin);
        btn_lregister = (Button)findViewById(R.id.btn_lregister);
 
        btn_lregister.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Login.this, MainActivity.class);
                startActivity(intent);
            }
        });
 
        btn_llogin.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String username = et_lusername.getText().toString();
                String password = et_lpassword.getText().toString();
 
                Boolean checklogin = databaseHelper.CheckLogin(username, password);
                if(checklogin == true){
                    Toast.makeText(getApplicationContext(), "Login Successful", Toast.LENGTH_SHORT).show();
                }else{
                    Toast.makeText(getApplicationContext(), "Invalid username or password", Toast.LENGTH_SHORT).show();
                }
            }
        });
    } 
