# CAMERA-APP
# MAD-PROJECT

## AIM:

Create an camera app using android studio.

## EQUIPMENTS REQUIRED:

Latest Version Android Studio

## ALGORITHM:
Step 1: Create a New Project in Android Studio

Step 2: Working with the activity_main.xml File

Step 3: Working with the MainActivity File

Step 4: Run the app

## PROGRAM:

/*

Developed by:Atchaya S
Registeration Number :212222040021
*/

# In MainActivity.java

java
package com.example.camerafull1;



import androidx.activity.result.ActivityResult;

import androidx.activity.result.ActivityResultCallback;

import androidx.activity.result.ActivityResultCaller;

import androidx.activity.result.ActivityResultLauncher;

import androidx.activity.result.contract.ActivityResultContracts;

import androidx.annotation.Nullable;

import androidx.appcompat.app.AppCompatActivity;

import androidx.core.content.FileProvider;


import android.annotation.SuppressLint;
import android.app.Activity;

import android.content.ContentResolver;

import android.content.Intent;

import android.graphics.Bitmap;

import android.media.Image;

import android.net.Uri;

import android.os.Bundle;

import android.os.Environment;

import android.provider.MediaStore;

import android.util.Log;

import android.util.Rational;

import android.util.Size;

import android.view.TextureView;

import android.view.View;

import android.widget.Button;

import android.widget.ImageView;

import android.widget.Toast;


import com.example.camerafull1.R;

import java.io.File;

import java.io.FileNotFoundException;

import java.io.FileOutputStream;

import java.io.IOException;

import java.lang.ref.WeakReference;



public class MainActivity extends AppCompatActivity {

    private static final int REQUEST_CODE = 22;

    Button btnpicture;

    ImageView imageView;

    ActivityResultLauncher<Intent> activityResultLauncher;



    @SuppressLint("MissingInflatedId")
    @Override

    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        btnpicture = findViewById(R.id.btncamera_id);

        imageView = findViewById(R.id.image);



        btnpicture.setOnClickListener(new View.OnClickListener() {

            @Override

            public void onClick(View v) {

                Intent cameraIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);

                activityResultLauncher.launch(cameraIntent);



            }

        });



        activityResultLauncher = registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), new ActivityResultCallback<ActivityResult>() {

            @Override

            public void onActivityResult(ActivityResult result) {



                Bundle extras = result.getData().getExtras();

                Uri imageUri;

                Bitmap imageBitmap = (Bitmap) extras.get("data");

                WeakReference<Bitmap> result_1 = new WeakReference<>(Bitmap.createScaledBitmap(imageBitmap,

                                imageBitmap.getWidth(), imageBitmap.getHeight(), false).

                        copy(Bitmap.Config.RGB_565, true));



                Bitmap bm = result_1.get();

                imageUri = saveImage(bm, MainActivity.this);

                imageView.setImageURI(imageUri);

            }

        });



    }



    private Uri saveImage(Bitmap image, MainActivity context) {

        File imagefolder = new File(context.getCacheDir(), "images");

        Uri uri = null;

        try{

            imagefolder.mkdirs();

            File file = new File(imagefolder, "captured_image.jpg");

            FileOutputStream stream = new FileOutputStream(file);

            image.compress(Bitmap.CompressFormat.JPEG, 100, stream);

            stream.flush();

            stream.close();

            uri = FileProvider.getUriForFile(context.getApplicationContext(), "com.allcodingtutorial.camerafull1"+".provider", file);

        }



        catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }

        return uri ;

    }



}







# In activity_main.xml
xml
<?xml version="1.0" encoding="utf-8"?>

<RelativeLayout

    xmlns:android="http://schemas.android.com/apk/res/android"

    xmlns:app="http://schemas.android.com/apk/res-auto"

    xmlns:tools="http://schemas.android.com/tools"

    android:layout_width="match_parent"

    android:layout_height="match_parent"

    android:layout_margin="10dp"

    tools:context=".MainActivity">



    <TextView

        android:id="@+id/text"

        android:layout_width="wrap_content"

        android:layout_height="wrap_content"

        android:text="Click on the camera button to start the camera"

        />



    <Button

        android:id="@+id/btncamera_id"

        android:layout_width="match_parent"

        android:layout_height="wrap_content"

        android:layout_below="@+id/text"

        android:text="Camera"

        android:layout_centerHorizontal="true"

        />



    <ImageView

        android:id="@+id/image"

        android:layout_width="match_parent"

        android:layout_height="match_parent"

        android:layout_below="@+id/btncamera_id"/>



</RelativeLayout>



## OUTPUT
![image](https://github.com/RANJEETH17/MAD--PROJECT/assets/120718823/3448b81f-92bd-43ba-aa32-3f2afa605bb2)
![image](https://github.com/RANJEETH17/MAD--PROJECT/assets/120718823/41f36113-1ddc-4dc5-ba6e-17223670e819)
![image](https://github.com/RANJEETH17/MAD--PROJECT/assets/120718823/be558e65-0957-483e-91e1-dd06cbd8cd06)










## RESULT
Thus simple camera Application using Android Studio is developed and executed successfully.
