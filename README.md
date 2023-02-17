# Smart-Agriculture-Weather-App
The application suitale for the farmers to cultivate their crops according to the weather and climate condition
package com.example.mysmartweatherapp;

import android.content.Intent;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import com.android.volley.Request;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;

import java.text.DecimalFormat;

public class MainActivity extends AppCompatActivity {

   EditText city_name;
   TextView tvresult;
  private Button updatebtn;
   private final String url ="http://api.openweathermap.org/data/2.5/weather";
   private final String appid="f9d69425eff5196bfc8d6f4f6c70851c";
   DecimalFormat df= new DecimalFormat("#.##");

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        city_name=findViewById(R.id.city_name);
        tvresult=findViewById(R.id.tvresult);
        updatebtn= (Button) findViewById(R.id.updatebtn);
        updatebtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ResultShowingActivity();
            }
        });





    }
    public void ResultShowingActivity(){
        Intent intent= new Intent(this, ResultShowingActivity.class);
        startActivity(intent);
    }


    public void getweatherupdate(View view) {
        String tempUrl="";
        String city=city_name.getText().toString().trim();
       if(city.equals("")){
           tvresult.setText("City field cannot be empty");
       }else{
           tempUrl=url + "?q=" + city + "," + "&appid=" +appid;
       }
        StringRequest stringRequest = new StringRequest(Request.Method.POST, tempUrl, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.d("response", response);

            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Toast.makeText(getApplicationContext(),error.toString().trim(),Toast.LENGTH_SHORT).show();
            }
        });
    }
}
