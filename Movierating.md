-----------------------------------------------------XMLCODE--------------------------------------------------------



<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/movieImageView"
        android:layout_width="150dp"
        android:layout_height="200dp"
        android:layout_gravity="center"
        />

    <RatingBar
        android:id="@+id/movieRatingBar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:numStars="6"
        android:stepSize="0.5" />

</LinearLayout>




-------------------------------------------MAINACTIVITY-------------------------------------------------------------


package com.example.movieratingapp;

import android.os.Bundle;
import android.widget.ImageView;
import android.widget.RatingBar;
import android.widget.Toast;
import androidx.annotation.DrawableRes;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private ImageView movieImageView;
    private RatingBar movieRatingBar;

    @DrawableRes
    private int[] moviePosters = {
            R.drawable.jj, R.drawable.jj1, R.drawable.another_movie, R.drawable.yet_another_movie
    };

    private int currentMovieIndex = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        movieImageView = findViewById(R.id.movieImageView);
        movieRatingBar = findViewById(R.id.movieRatingBar);

        updateMoviePoster(currentMovieIndex);

        movieRatingBar.setOnRatingBarChangeListener((ratingBar, rating, fromUser) -> {
            if (fromUser) {
                currentMovieIndex = (currentMovieIndex + 1) % moviePosters.length;
                updateMoviePoster(currentMovieIndex);
                String ratingMessage = "You rated this movie " + rating + " stars!";
                Toast.makeText(this, ratingMessage, Toast.LENGTH_SHORT).show();
            }
        });
    }

    private void updateMoviePoster(int index) {
        movieImageView.setImageResource(moviePosters[index]);
        movieRatingBar.setRating(0);
    }
}

