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

![6주차 3번째](https://user-images.githubusercontent.com/79956770/116978847-3887e480-acff-11eb-947a-0ba5a8b4ceae.JPG)
public class MainActivity extends AppCompatActivity {

    private RecyclerView recyclerView;
    private RecyclerView.Adapter adapter;
    private RecyclerView.LayoutManager layoutManager;
    private ArrayList<User> arrayList;
    private FirebaseDatabase database;
    private DatabaseReference databaseReference;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        recyclerView = findViewById(R.id.recyclerView); // 아이디 연결
        recyclerView.setHasFixedSize(true); 
        layoutManager = new LinearLayoutManager(this);
        recyclerView.setLayoutManager(layoutManager);
        arrayList = new ArrayList<>(); // User객체를 담을 arraylist (adapt쪽으로)

        database = FirebaseDatabase.getInstance(); //파이어베이스 데이터베이스 연동

        databaseReference = database.getReference("User"); // DB 테이블 연결
        databaseReference.addListenerForSingleValueEvent(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                // 파이어베이스 데이터베이스의 데이터를 받아오는 곳
                arrayList.clear(); // 기존 배열 리스트가 존재하지 않게 초기화
                for (DataSnapshot snapshot : dataSnapshot.getChildren()) { //반복문으로 데이터 리스트를 추출
                    User user = snapshot.getValue(User.class); // 만들어졌던 User 객체에 데이터를 담는다
                    arrayList.add(user); // 담은 데이터들을 배열리스트에 넣고 리사이클러뷰로 보낼 준비
                }
                adapter.notifyDataSetChanged(); // 리스트 저장 및 새로고침


            }

            @Override
            public void onCancelled(@NonNull DatabaseError databaseError) {
            }
        });

        adapter = new CustomAdapter(arrayList, this);
        recyclerView.setAdapter(adapter); //리사이클러뷰에 어댑터 연결

    }
}




