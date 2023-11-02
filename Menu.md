package com.example.main;

----------------------------------------->   RES(Directory)---->  Res file --------> menu ------->    


-----------------------------------MENUXML-------------------------------------------------------------------------

<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/menu_item_1"
        android:title="Item 1">
    </item>
    <item
        android:id="@+id/menu_item_2"
        android:title="Item 2">
        <menu>
            <item
                android:id="@+id/submenu_item_1"
                android:title="Subitem 1">
            </item>
            <item
                android:id="@+id/submenu_item_2"
                android:title="Subitem 2">
            </item>
        </menu>
    </item>
</menu>



----------------->Res------->Values-------->  themes---------------------------------------------------------------

remove .noActionbar



















--------------------------------------------------MAINACTIVITY------------------------------------------------------

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    @Override
    public boolean onCreateOptionsMenu(Menu menu){
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.menu, menu);
        return true;
    }
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        Toast.makeText(this, "Selected Item: " + item.getTitle(), Toast.LENGTH_SHORT)
                .show();
        return true;
    }
}