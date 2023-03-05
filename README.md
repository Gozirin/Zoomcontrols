# Zoomcontrols
ZoomControls in which we display an ImageView and a ZoomControls. In this first we hide the ZoomControls from the screen and show it on the touch event of image. We also perform setOnZoomInClickListener and setOnZoomOutClickListener events for implementing zoom in and zoom out functionality.
After zoom in and zoom out the ZoomControls is automatically hide from the screen and re-shown if user click on the image. A Toast is displayed to show the zoom in and zoom out message on the screen.

<img width="269" alt="s1" src="https://user-images.githubusercontent.com/95639970/222970464-5fbe3580-64c2-4307-aafa-69216f8de858.png"> <img width="269" alt="s2" src="https://user-images.githubusercontent.com/95639970/222970496-e5e25b36-6525-4b38-974f-eccd5d7ae8da.png">
<img width="269" alt="s3" src="https://user-images.githubusercontent.com/95639970/222970504-c7b53c54-8d7f-482e-b225-6305f4e07a13.png">

In this step we add the code for displaying a ImageView and ZoomControls.

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:background="#000"
android:paddingBottom="@dimen/activity_vertical_margin"
android:paddingLeft="@dimen/activity_horizontal_margin"
android:paddingRight="@dimen/activity_horizontal_margin"
android:paddingTop="@dimen/activity_vertical_margin"
tools:context=".MainActivity">

<ImageView
android:id="@+id/image"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_centerInParent="true"
android:src="@drawable/image" />

<ZoomControls
android:id="@+id/simpleZoomControl"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_alignParentBottom="true"
android:layout_centerHorizontal="true"
android:layout_marginTop="50dp" />

</RelativeLayout>

We also perform setOnZoomInClickListener and setOnZoomOutClickListener events for implementing zoom in and zoom out functionality. After zoom in and zoom out the ZoomControls is automatically hide from the screen and for re-showing it user need to click on image. A Toast is displayed to show the zoom in and zoom out message on the screen.

package example.abhiandroid.zoomcontrolsexample;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.Menu;
import android.view.MenuItem;
import android.view.MotionEvent;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.Toast;
import android.widget.ZoomControls;

public class MainActivity extends AppCompatActivity {

    ImageView image;
    ZoomControls simpleZoomControls;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        image = (ImageView) findViewById(R.id.image); // initiate a ImageView
        simpleZoomControls = (ZoomControls) findViewById(R.id.simpleZoomControl); // initiate a ZoomControls
        simpleZoomControls.hide(); // initially hide ZoomControls from the screen
        // perform setOnTouchListener event on ImageView
        image.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                // show Zoom Controls on touch of image
                simpleZoomControls.show();
                return false;
            }
        });
        // perform setOnZoomInClickListener event on ZoomControls
        simpleZoomControls.setOnZoomInClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // calculate current scale x and y value of ImageView
                float x = image.getScaleX();
                float y = image.getScaleY();
                // set increased value of scale x and y to perform zoom in functionality
                image.setScaleX((float) (x + 1));
                image.setScaleY((float) (y + 1));
                // display a toast to show Zoom In Message on Screen
                Toast.makeText(getApplicationContext(),"Zoom In",Toast.LENGTH_SHORT).show();
                // hide the ZoomControls from the screen
                simpleZoomControls.hide();
            }
        });
        // perform setOnZoomOutClickListener event on ZoomControls
        simpleZoomControls.setOnZoomOutClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // calculate current scale x and y value of ImageView
                float x = image.getScaleX();
                float y = image.getScaleY();
                // set decreased value of scale x and y to perform zoom out functionality
                image.setScaleX((float) (x - 1));
                image.setScaleY((float) (y - 1));
                // display a toast to show Zoom Out Message on Screen
                Toast.makeText(getApplicationContext(),"Zoom Out",Toast.LENGTH_SHORT).show();
                // hide the ZoomControls from the screen
                simpleZoomControls.hide();
            }
        });
    }


}
