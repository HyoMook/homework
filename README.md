# homework
# 안드로이드 앱 구동화면
![201721185 윤효묵 안드로이드 앱 구동화면](https://user-images.githubusercontent.com/79956770/110571181-86b6b680-819a-11eb-996c-a64fbf9a07a0.JPG)

# In-class Homework Week 2 Day 1 #1
# 화면 출력 문자열 변경
![201721185 윤효묵 화면 출력 문자열 변경](https://user-images.githubusercontent.com/79956770/110571272-a8b03900-819a-11eb-9bd5-510162855cb9.JPG)

# In-class Homework Week 2 Day 2 #1
# git 연결
![201721185 윤효묵 git 연결](https://user-images.githubusercontent.com/79956770/110786068-0c2b8b00-82af-11eb-834f-1f3d877a15ec.JPG)

# In-class Homework Week 3 Day 1 #1
# Activity Lifecycle in Action
![201721185 윤효묵 lifecycle 과제](https://user-images.githubusercontent.com/79956770/111563069-99ed0600-87da-11eb-8d62-8269e1134a0e.JPG)

교수님, 애뮬레이터 안 나온다고 html 파일에 적었는데, 문제 고쳐서 잘 나옵니다^^

https://www.youtube.com/watch?v=70Q4un2AR7k

```
package org.techtown.mypictureproject;

import androidx.appcompat.app.ActionBar;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;

import android.content.Intent;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.widget.ImageView;

public class FullScreenActivity extends AppCompatActivity {

    ImageView imageView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_full_screen);

        imageView = (ImageView) findViewById(R.id.image_view);

        //getSupportActionBar() .hide();
        //getSupportActionBar() .setTitle("Full Screen Image");

        Intent i = getIntent();
        int position = i.getExtras().getInt("id");
        ImageAdapter imageAdapter = new ImageAdapter(this);

        imageView.setImageResource(imageAdapter.imageArray[position]);

        Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        ActionBar actionBar = getSupportActionBar();
        actionBar.setDisplayShowCustomEnabled(true);
        actionBar.setDisplayShowTitleEnabled(false);
        actionBar.setDisplayHomeAsUpEnabled(true);
    }
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuInflater menuInflater = getMenuInflater();
        menuInflater.inflate(R.menu.menu_main,menu);
        return super.onCreateOptionsMenu(menu);
    }
}```



