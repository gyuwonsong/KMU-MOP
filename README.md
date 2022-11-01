# 2022-2 모바일 프로그래밍 개인 프로젝트
소프트웨어학부 20213015 송규원

## 목차
1. 프로젝트 설명
- 1-1. 프로젝트 개요
- 1-2. 소스파일 구성
- 1-3. 개발환경 및 실행 환경


2. UI 설계
- 2-1. 첫 번째 화면 (Home)
- 2-2. 두 번째 화면 (favorite)
- 2-3. 세 번째 화면 (User)

3. 구현 내용
- 3-1. Activity
- 3-2. Fragment
- 3-3. Java

## 1. 프로젝트 설명
### 1-1. 프로젝트 개요
앱 시작 시, 5개 이상의 상품을 화면에 출력하고 네비게이션의 각 아이템 클릭 시 프래그먼트를 교체하고 필요에 따라 액티비티를 호출하는 방식을 사용하여 구현하였다.

### 1-2. 소스파일 구성 
|파일명|역할|
|------|---|
|DBHelper.java|데이터 베이스 구축을 위한 소스파일|
|MainActivity.java|가장 처음으로 실행되는 메인 액티비티|
|SigninActivity.java|로그인 기능을 구현해둔 소스파일|
|SignupActivity.java|회원가입 기능을 구현해둔 소스파일|
|HomeFragment.java|홈 화면에 대한 프래그먼트|
|FavoriteFragment.java|찜 한 목록에 대한 프래그먼트|
|SigninFragment.java|로그인/ 회원가입 창으로 이동할 수 있는 프래그먼트|

### 1-3. 개발환경 및 실행 환경
- Language : Java
- IDE : Android Studio
- 실행환경 : SDK 버전은 안드로이드 12를 사용

## 2. UI 설계
|파일명|연결|역할|
|------|---|---|
|activity_main.xml|MainActivity.java|가장 처음으로 실행되는 메인 액티비티에 연결되는 레이아웃|
|activity_signin.xml|SigninActivity.java|로그인 화면에 대한 레이아웃|
|activity_signup.xml|SignupActivity.java|회원가입 화면에 대한 레이아웃|
|fragment_home.xml|HomeFragment.java|홈 화면(상품 리스트)에 대한 레이아웃|
|fragment_favorite.xml|FavoriteFragment.java|찜 한 목록에 대한 레이아웃|
|fragment_signin.xml|SigninFragment.java|로그인/ 회원가입 창으로 이동할 수 있는 레이아웃|

### 2-1. 첫 번째 화면 (fragment_home.xml)
첫 번째 화면은 5개 이상의 상품 리스트를 보여준다. 화면과 화면 간의 전환은 전체적으로 네비게이션을 사용하였다. 찜 버튼을 추가하면 찜 한 목록(두 번째 화면)에 추가되도록 구현하고 싶었지만 로그인 및 회원가입 기능에 초점을 두어 구현하지 못했다.

<img src="https://user-images.githubusercontent.com/81706832/199233921-d6ee3434-6e55-4110-b17b-66871f38b6ba.png" width="210" height="400"/>

#### 2-1-1. 레이아웃
전체적으로 FrameLayout을 사용하였고, constraintlayout을 사용하여 크게 묶은 후 ScrollView를 사용하여 스크롤이 가능하도록 했다. ScrollView는 하나의 레이아웃 만을 포함하고 있어야 해서 LinearLayout을 사용하여 크게 묶고, 각 상품에 대한 세부적인 레이아웃을 RelativeLayout을 사용하여 이미지와 버튼 및 텍스트 등을 포함하게 했다. 
'''
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HomeFragment">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:scrollbars="vertical" >

        <ScrollView
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:scrollbarFadeDuration = "0"
            android:scrollbarAlwaysDrawVerticalTrack = "true"
            android:scrollbarSize="5dp"
            tools:ignore="MissingConstraints" >

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                tools:ignore="MissingConstraints"
                android:orientation="vertical">

                <RelativeLayout
                    android:id="@+id/p1"
                    android:layout_width="match_parent"
                    android:layout_height="150dp"
                    android:elevation="10dp"
                    tools:ignore="MissingConstraints" >

### 2-2. 두 번째 화면 (favorite)
구현계획대로라면 첫 번째 화면에서 찜 버튼을 클릭하면 해당 화면으로 데이터가 넘어오게끔 구현하고 싶었으나 로그인 및 회원가입 기능에 치중을 두어 구현하지 못했다. xml파일에 임의로 데이터를 넣는 것을 통해 일단 구현해 둔 상태이고, 이 부분은 다시 시도해볼 예정이다.

<img src="https://user-images.githubusercontent.com/81706832/199236178-38614530-7fcd-4ccf-ab98-5eadd62fbfca.png" width="210" height="400"/>

#### 2-2-1. 레이아웃
전체적으로 LinearLayout을 사용하였고, 그 안에 또 LinearLayout으로 한 번 묶은 후 각 상품에 대한 이미지 및 텍스트 등을 RelativeLayout으로 묶어 구현하였다. 
'''
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".FavoriteFragment">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <RelativeLayout
            android:id="@+id/p3"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:elevation="10dp"
            tools:ignore="MissingConstraints"
            tools:layout_editor_absoluteX="0dp"
            tools:layout_editor_absoluteY="50dp">
            
### 2-3. 세 번째 화면 (User)
가장 핵심적인 기능이 구현되어 있는 프래그먼트이다. 먼저, 기존에 회원가입이 되어있는 회원이라면 로그인 버튼을 클릭할 수 있고 회원가입이 되어있지 않다면 회원가입을 할 수 있는 버튼을 만들어 두었다. 기본적으로 회원가입 없이 모든 기능을 가능하게끔 구현하였고, 프래그먼트에서는 로그인 및 회원가입 정보에 대한 데이터 전달이 원활하게 되지 않아 버튼을 누르면 각 액티비티로 이동할 수 있게끔 동적 코드를 구현하였다.

<img src="https://user-images.githubusercontent.com/81706832/199237314-8610acca-63d8-45ca-a2c2-6c43d8f3786f.png" width="210" height="400"/>

#### 2-3-1. 레이아웃
비교적 단순하게 단일 레이아웃으로만 구성하였다. 사용한 레이아웃은 LinearLayout이다.


## 3. 구현 내용
### 3-1. Activity
<img src="https://user-images.githubusercontent.com/81706832/199242348-711b019c-8f3e-4193-aea3-151398f72b80.png" width="210" height="400"/>
<img src="https://user-images.githubusercontent.com/81706832/199242422-02adf489-da67-4871-9d7f-8b5174a37213.png" width="210" height="400"/>
액티비티는 총 3개이다. 메인, 로그인, 회원가입인데, 전체적인 구성은 프래그먼트로 하여 메인 액티비티에 필요 시에 맞는 프래그먼트를 호출하는 방식이다. 로그인과 회원가입은 프래그먼트에서 정보 저장을 할 수 없어 프래그먼트에서 각 액티비티를 호출하는 방식으로 구현하였다.

### 3-2. Fragment
프래그먼트는 home, favorite, user로 총 3개이다. 해결하지 못한 부분이 있는데, 초기 앱 실행 시 유저 버튼을 누르면 기존 signinFragment를 띄우는 것이 정상이다. 하지만 만약 로그인 액티비티를 통해 로그인을 마치고 온 상황이라면 유저 버튼을 눌렀을 때 회원 정보에 대한 목록을 띄워주는 프래그먼트가 나와야 하는데 이 부분을 미처 다 구현하지 못했다. 플래그 변수를 사용하여 함수 호출하는 방식으로 해보려 했지만 해결하지 못해서 프로잭트를 마치는 것과 별개로 다시 시도해 볼 생각이다. 

### 3-3. Java
Java 파일은 총 7개인데, 여기서 핵심적으로 봐야 할 부분은 MainActivity.java, SigninFragment.java, SigninActivity.java, SignupActivity.java이다.

#### 3-3-1. MainActivity.java
bottomnavigation의 아이템마다 프래그먼트가 전환되는 부분을 구현한 코드이다. 프래그먼트 변경 시 switch~case 문을 사용한 함수를 따로 구현하였다.

'''
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottomNavigationView = findViewById(R.id.nav_view);
        bottomNavigationView.setOnNavigationItemSelectedListener(new BottomNavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem menuItem) {
                switch (menuItem.getItemId()) {
                    case R.id.homeId:
                        setFrag(0);
                        break;
                    case R.id.favoriteId:
                        setFrag(1);
                        break;
                    case R.id.userId:
                        setFrag(2);
                        break;
                }
                return true;
            }
        });

        homeFragment = new HomeFragment();
        favoriteFragment = new FavoriteFragment();
        signinFragment = new SigninFragment();
        setFrag(0);
    }

    public void setFrag(int n) {
        fm = getSupportFragmentManager();
        ft= fm.beginTransaction();
        switch (n)
        {
            case 0:
                ft.replace(R.id.mainFramelayout, homeFragment);
                ft.commit();
                break;

            case 1:
                ft.replace(R.id.mainFramelayout, favoriteFragment);
                ft.commit();
                break;

            case 2:
                ft.replace(R.id.mainFramelayout, signinFragment);
                ft.commit();
                break;
        }
    }
    
#### 3-3-2. SigninFragment.java
가장 많은 시간을 들인 자바 코드이다. 액티비티 <-> 액티비티 간의 인텐트와 프래그먼트 <-> 액티비티의 인텐트가 달라 getActivity() 함수를 사용하였다.

'''
public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        view = (View) inflater.inflate(R.layout.fragment_signin, container, false);

        toSignIn = (Button) view.findViewById(R.id.toSignIn);
        toSignUp = (Button) view.findViewById(R.id.toSignUp);

        toSignIn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(getActivity(), SigninActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_NO_ANIMATION);
                startActivity(intent);
            }
        });

        toSignUp.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(getActivity(), SignupActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_NO_ANIMATION);
                startActivity(intent);
            }
        });

        return view;
    }
    
#### 3-3-3. SigninActivity.java
로그인 버튼을 누르면 존재하지 않는 아이디인지, 비밀번호를 틀렸는지에 대해 검사해 준다. 그리고 홈화면으로 돌아온다.
            
'''
@Override
            public void onClick(View view) {
                String id = id_value.getText().toString();
                String pw = pw_value.getText().toString();

                //공백 확인
                if (id.length() == 0 || pw.length() == 0) {
                    Toast toast = Toast.makeText(SigninActivity.this, "아이디와 비밀번호를 입력해 주세요.", Toast.LENGTH_SHORT);
                    toast.show();
                    return;
                }

                sql = "SELECT id FROM "+ dbHelper.tableName + " WHERE id = '" + id + "'";
                cursor = db.rawQuery(sql, null);

                //아이디 틀린 경우
                if(cursor.getCount()!=1){
                    Toast toast = Toast.makeText(SigninActivity.this, "존재하지 않는 아이디입니다.", Toast.LENGTH_SHORT);
                    toast.show();
                    return;
                }

                sql = "SELECT pw FROM "+ dbHelper.tableName + " WHERE id = '" + id + "'";
                cursor = db.rawQuery(sql, null);

                cursor.moveToNext();
                //비밀번호 틀린 경우
                if(!pw.equals(cursor.getString(0))){
                    Toast toast = Toast.makeText(SigninActivity.this, "비밀번호를 다시 확인해 주세요.", Toast.LENGTH_SHORT);
                    toast.show();
                }
                //문제 없으면 로그인 완료
                else{
                    Toast toast = Toast.makeText(SigninActivity.this, "Succeed Sign In!", Toast.LENGTH_SHORT);
                    toast.show();

                    mainActivity.setFrag(0);

                    Intent intent = new Intent(SigninActivity.this, SigninActivity.class);
                    startActivity(intent);
                    finish();
                }
                cursor.close();
            }
            
#### 3-3-4. SignupActivity.java
회원가입 버튼을 누르면 아이디 중복검사, 비밀번호 규칙, 전화번호 입력 규칙 등에 대한 Toast를 띄워준다. 해당 사항이 없다면 회원가입을 할 수 있도록 해두었고 데이터 베이스에 이를 저장한다. 또, 개인정보 약관 동의에 대한 약관 보기를 클릭하면 개인정보 약관을 AlertDialog에 담아 띄울 수 있도록 구현하였다.

'''
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_signup);

        et_id = (EditText) findViewById(R.id.et_id);
        et_pw = (EditText) findViewById(R.id.et_pw);
        et_name = (EditText) findViewById(R.id.et_name);
        et_hp = (EditText) findViewById(R.id.et_hp);
        et_address = (EditText) findViewById(R.id.et_adress);

        btn_Join = (Button) findViewById(R.id.btn_Join);
        btn_Tos = (Button) findViewById(R.id.btn_Tos);

        dbHelper = new DBHelper(SignupActivity.this, DBHelper.tableName,null,version);
        database = dbHelper.getWritableDatabase();

        //회원가입
        btn_Join.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String id = et_id.getText().toString();
                String pw = et_pw.getText().toString();
                String hp = et_hp.getText().toString();

                //공백 학인
                if (id.length() == 0 || pw.length() == 0) {
                    Toast toast = Toast.makeText(SignupActivity.this, "아이디와 비밀번호를 입력해 주세요.", Toast.LENGTH_SHORT);
                    toast.show();
                    return;
                }

                sql = "SELECT id FROM " + dbHelper.tableName + " WHERE id = '" + id + "'";
                cursor = database.rawQuery(sql,null);

                //아이디 중복 확인
                if(cursor.getCount() != 0){
                    Toast toast = Toast.makeText(SignupActivity.this,"이미 존재하는 아이디입니다.", Toast.LENGTH_SHORT);
                    toast.show();
                }
                //비밀번호 확인
                if(!Pattern.matches("^(?=.*[A-Za-z])(?=.*[0-9])(?=.*[$@$!%*#?&]).{6,15}.$", pw)){
                    Toast toast = Toast.makeText(SignupActivity.this,"영문, 숫자, 특수기호를 모두 포함하여 6~15자 이내로 입력해 주세요", Toast.LENGTH_SHORT);
                    toast.show();
                }
                //전화번호 확인
                if(!Pattern.matches("^01(?:0|1|[6-9])(?:\\d{3}|\\d{4})\\d{4}$", hp)){
                    Toast toast = Toast.makeText(SignupActivity.this,"올바른 휴대폰 번호가 아닙니다.", Toast.LENGTH_SHORT);
                    toast.show();
                }
                //문제 없으면 회원가입 완료
                else{
                    dbHelper.insertUser(database, id, pw);

                    Toast toast = Toast.makeText(SignupActivity.this,"Succeed Sign Up!", Toast.LENGTH_SHORT);
                    toast.show();

                    mainActivity.setFrag(0);

                    Intent intent = new Intent(getApplicationContext(), MainActivity.class);
                    startActivity(intent);
                    finish();
                }
            }
        });


        //개인정보 활용 약관 보기
        btn_Tos.setOnClickListener(new View.OnClickListener() {

            String text = "<개인정보보호 포털> 개인정보 처리방침\n" +
                    "개인정보보호위원회가 취급하는 모든 개인정보는 관련 법령에 근거하여 수집 · 보유 및 처리되고 있습니다. 「개인정보보호법」은 이러한 개인정보의 취급에 대한 일반적 규범을 제시하고 있으며, 개인정보보호위원회는 이러한 법령의 규정에 따라 수집 · 보유 및 처리하는 개인정보를 공공업무의 적절한 수행과 이용자의 권익을 보호하기 위해 적법하고 적정하게 취급할 것입니다.\n" +
                    "\n" +
                    "또한, 개인정보보호위원회는 관련 법령에서 규정한 바에 따라 보유하고 있는 개인정보에 대한 열람, 정정·삭제, 처리정지 요구 등 이용자의 권익을 존중하며, 이용자는 이러한 법령상 권익의 침해 등에 대하여 행정심판법에서 정하는 바에 따라 행정심판을 청구할 수 있습니다.\n" +
                    "\n" +
                    "개인정보보호위원회는 개인정보보호법 제 30조에 따라 정보주체의 개인정보 보호 및 권익을 보호하고 개인정보와 관련한 이용자의 고충을 원활하게 처리할 수 있도록 다음과 같은 개인정보 처리방침을 수립 · 공개하고 있습니다.\n" +
                    "\n" +
                    "제1조 (개인정보의 처리 목적)\n" +
                    "\n" +
                    "① 개인정보보호위원회는 개인정보를 다음의 목적을 위해 처리합니다. 처리한 개인정보는 다음의 목적이외의 용도로는 사용되지 않으며 이용 목적이 변경되는 경우에는 개인정보 보호법 제18조에 따라 별도의 동의를 받는 등 필요한 조치를 이행할 예정입니다.\n" +
                    "가. 서비스 제공\n" +
                    "교육 콘텐츠 제공, 본인인증, 증명서발급(교육 수료증) 등 서비스 제공에 관련한 목적으로 개인정보를 처리합니다. \n" +
                    "협박 사례를 적극 신고하시기 바랍니다.\n" +
                    "나. 민원처리\n" +
                    "개인정보 열람, 개인정보 정정·삭제, 개인정보 처리정지 요구, 개인정보 유출사고 신고 등 개인정보와 관련된 민원처리를 목적으로 개인정보를 처리합니다.\n" +
                    "② 개인정보보호위원회가 개인정보 보호법 제32조에 따라 등록·공개하는 개인정보파일의 처리목적은 다음과 같습니다.";

            @Override
            public void onClick(View view) {
                AlertDialog.Builder builder = new AlertDialog.Builder(SignupActivity.this);
                builder.setTitle("개인정보 활용 동의 약관");
                builder.setMessage(text);
                builder.setPositiveButton("확인", null);
                builder.create().show();
            }
        });
    }
