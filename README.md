# Menu-item-handling-
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:padding="16dp">

   <!-- A ListView to show the menu items -->
   <ListView
       android:id="@+id/menuListView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:divider="@android:color/darker_gray"
       android:dividerHeight="1dp"
       android:padding="8dp" />

</RelativeLayout>
 
AndroidManifest.xml:
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
   package="com.example.menuapp">

   <application
       android:allowBackup="true"
       android:icon="@mipmap/ic_launcher"
       android:label="@string/app_name"
       android:theme="@style/Theme.AppCompat.Light.DarkActionBar">

       <!-- Main Activity -->
       <activity android:name=".MainActivity"
           android:exported="true">
           <intent-filter>
               <action android:name="android.intent.action.MAIN" />
               <category android:name="android.intent.category.LAUNCHER" />
           </intent-filter>
       </activity>

   </application>

</manifest>
 
MainActivity.java:
package com.example.menuapp;

import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

   private ListView menuListView;

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       menuListView = findViewById(R.id.menuListView);
   }

   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
       // Inflate the menu resource file to populate the menu
       getMenuInflater().inflate(R.menu.menu_main, menu);
       return true;
   }

   @Override
   public boolean onOptionsItemSelected(MenuItem item) {
       // If the "Show Menu" button is clicked, display the list of menu items
       if (item.getItemId() == R.id.action_menu) {
           // Create an array of menu items
           String[] menuItems = {"New", "Open", "Save"};

           // Set up an ArrayAdapter to display the menu items in the ListView
           ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, menuItems);
           menuListView.setAdapter(adapter);

           // Set an item click listener to show a Toast when a menu item is clicked
           menuListView.setOnItemClickListener((parent, view, position, id) -> {
               String clickedItem = menuItems[position];
               Toast.makeText(MainActivity.this, "Menu Item: " + clickedItem, Toast.LENGTH_SHORT).show();
           });

           return true;
       }

       return super.onOptionsItemSelected(item);
   }
}
 
Menu_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto">

   <item
       android:id="@+id/action_menu"
       android:title="Show Menu"
       app:showAsAction="ifRoom" />
</menu>
