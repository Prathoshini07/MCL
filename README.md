# MCL

package com.example.chumma

import android.annotation.SuppressLint
import android.icu.text.SimpleDateFormat
import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.EditText
import android.widget.ProgressBar
import android.widget.RatingBar
import android.widget.TextView
import androidx.annotation.RequiresApi
import java.time.LocalDate
import java.util.Date
import java.util.Locale

class MainActivity : AppCompatActivity() {
    @RequiresApi(Build.VERSION_CODES.O)
    @SuppressLint("MissingInflatedId")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val progressBar = findViewById<ProgressBar>(R.id.progressBar)
        val ratingBar = findViewById<RatingBar>(R.id.ratingBar)
        val tv = findViewById<TextView>(R.id.textView)
        val et = findViewById<EditText>(R.id.editTextText)
        progressBar.progress=50
        ratingBar.stepSize= 0.5F
        ratingBar.rating= 1.5F

        val sdf = SimpleDateFormat("yyyy-MM-dd", Locale.getDefault())
        val currentDate = sdf.format(Date())
        tv.text=currentDate.toString()

        val from_date=findViewById<EditText>(R.id.editTextDate)
        val to_date=findViewById<EditText>(R.id.editTextDate2)
        val button=findViewById<Button>(R.id.button)
        val tv=findViewById<TextView>(R.id.textView3)
        val dateFormat=SimpleDateFormat("dd/MM/yyyy", Locale.getDefault())
        button.setOnClickListener()
        {
            val fromdatestr=from_date.text.toString()
            val todatestr=to_date.text.toString()
            if(fromdatestr.isNotEmpty() && todatestr.isNotEmpty())
            {
                val from=dateFormat.parse(fromdatestr)
                val to=dateFormat.parse(todatestr)
                if(from!=null && to!=null)
                {
                    val diffinmillis=to.time-from.time
                    val days=TimeUnit.MILLISECONDS.toDays(diffinmillis).toInt()
                    val years=days/365
                    val months=(days%365)/30
                    val days_remaining=(days%365)%30
                    tv.text="years $years \n months $months \n days $days_remaining \n"
                }
            }
        }

    }
}
