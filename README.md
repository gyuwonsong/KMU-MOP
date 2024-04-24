## 2022-2 모바일 프로그래밍 개인 프로젝트
소프트웨어학부 20213015 송규원

## 목차
1. [프로젝트 설명](#프로젝트-설명)
   - 1.1 [프로젝트 개요](#프로젝트-개요)
   - 1.2 [소스파일 구성](#소스파일-구성)
   - 1.3 [개발환경 및 실행 환경](#개발환경-및-실행-환경)

2. [UI 설계](#UI-설계)
   - 2.1 [첫 번째 화면 (Home)](#첫-번째-화면-Home)
   - 2.2 [두 번째 화면 (favorite)](#두-번째-화면-favorite)
   - 2.3 [세 번째 화면 (User)](#세-번째-화면-User)

3. [구현 내용](#구현-내용)
   - 3.1 [Activity](#Activity)
   - 3.2 [Fragment](#Fragment)
   - 3.3 [Java](#Java)

---

## 프로젝트 설명

### 프로젝트 개요
앱 시작 시, 5개 이상의 상품을 화면에 출력하고 네비게이션의 각 아이템 클릭 시 프래그먼트를 교체하고 필요에 따라 액티비티를 호출하는 방식을 사용하여 구현하였다.

### 소스파일 구성 
| 파일명            | 역할                 |
|-----------------|---------------------|
| DBHelper.java   | 데이터 베이스 구축을 위한 소스파일 |
| MainActivity.java | 가장 처음으로 실행되는 메인 액티비티 |
| SigninActivity.java | 로그인 기능을 구현해둔 소스파일 |
| SignupActivity.java | 회원가입 기능을 구현해둔 소스파일 |
| HomeFragment.java | 홈 화면에 대한 프래그먼트 |
| FavoriteFragment.java | 찜 한 목록에 대한 프래그먼트 |
| SigninFragment.java | 로그인/ 회원가입 창으로 이동할 수 있는 프래그먼트 |

### 개발환경 및 실행 환경
- Language: Java
- IDE: Android Studio
- 실행환경: SDK 버전은 안드로이드 12를 사용

---

## UI 설계

### 첫 번째 화면 (Home)
첫 번째 화면은 5개 이상의 상품 리스트를 보여준다. 화면과 화면 간의 전환은 전체적으로 네비게이션을 사용하였다. 찜 버튼을 추가하면 찜 한 목록(두 번째 화면)에 추가되도록 구현하고 싶었지만 로그인 및 회원가입 기능에 초점을 두어 구현하지 못했다.

<img src="https://user-images.githubusercontent.com/81706832/199233921-d6ee334-6e55-4110-b17b-66871f38b6ba.png" width="210" height="400"/>

#### 레이아웃
전체적으로 `FrameLayout`을 사용하였고, `ConstraintLayout`을 사용하여 크게 묶은 후 `ScrollView`를 사용하여 스크롤이 가능하도록 했다. `ScrollView`는 하나의 레이아웃 만을 포함하고 있어야 해서 `LinearLayout`을 사용하여 크게 묶고, 각 상품에 대한 세부적인 레이아웃을 `RelativeLayout`을 사용하여 이미지와 버튼 및 텍스트 등을 포함하게 했다. 

```xml
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
        android:scrollbars="vertical">

        <ScrollView
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:scrollbarFadeDuration="0"
            android:scrollbarAlwaysDrawVerticalTrack="true"
            android:scrollbarSize="5dp"
            tools:ignore="MissingConstraints">

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
                    tools:ignore="MissingConstraints">
```

### 두 번째 화면 (favorite)
구현계획대로라면 첫 번째 화면에서 찜 버튼을 클릭하면 해당 화면으로 데이터가 넘어오게끔 구현하고 싶었으나 로그인 및 회원가입 기능에 치중을 두어 구현하지 못했다. xml 파일에 임의로 데이터를 넣는 것을 통해 일단 구현해 둔 상태이고, 이 부분은 다시 시도해볼 예정이다.

<img src="https://user-images.githubusercontent.com/81706832/199236178-38614530-7fcd-4ccf-ab98-5eadd62fbfca.png" width="210" height="400"/>

#### 레이아웃
전체적으로 `LinearLayout`을 사용하였고, 그 안에 또 `LinearLayout`으로 한 번 묶은 후 각 상품에 대한 이미지 및 텍스트 등을 `RelativeLayout`으로 묶어 구현하였다. 

```

xml
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
```

### 세 번째 화면 (User)
가장 핵심적인 기능이 구현되어 있는 프래그먼트이다. 먼저, 기존에 회원가입이 되어있는 회원이라면 로그인 버튼을 클릭할 수 있고 회원가입이 되어있지 않다면 회원가입을 할 수 있는 버튼을 만들어 두었다. 기본적으로 회원가입 없이 모든 기능을 가능하게끔 구현하였고, 프래그먼트에서는 로그인 및 회원가입 정보에 대한 데이터 전달이 원활하게 되지 않아 버튼을 누르면 각 액티비티로 이동할 수 있게끔 동적 코드를 구현하였다.

<img src="https://user-images.githubusercontent.com/81706832/199237314-8610acca-63d8-45ca-a2c2-6c43d8f3786f.png" width="210" height="400"/>

#### 레이아웃
비교적 단순하게 단일 레이아웃으로만 구성하였다. 사용한 레이아웃은 `LinearLayout`이다.

---

## 구현 내용

### Activity

<img src="https://user-images.githubusercontent.com/81706832/199242348-711b019c-8f3e-4193-aea3-151398f72b80.png" width="210" height="400"/>
<img src="https://user-images.githubusercontent.com/81706832/199242422-02adf489-da67-4871-9d7f-8b5174a37213.png" width="210" height="400"/>

액티비티는 총 3개이다. 메인, 로그인, 회원가입인데, 전체적인 구성은 프래그먼트로 하여 메인 액티비티에 필요 시에 맞는 프래그먼트를 호출하는 방식이다. 로그인과 회원가입은 프래그먼트에서 정보 저장을 할 수 없어 프래그먼트에서 각 액티비티를 호출하는 방식으로 구현하였다.

#### MainActivity.java
bottomnavigation의 아이템마다 프래그먼트가 전환되는 부분을 구현한 코드이다. 프래그먼트 변경 시 switch~case 문을 사용한 함수를 따로 구현하였다.

```java
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
```

#### SigninFragment.java
가장 많은 시간을 들인 자바 코드이다. 액티비티 <-> 액티비티 간의 인텐트와 프래그먼트 <-> 액티비티의 인텐트가 달라 getActivity() 함수를 사용하였다.

```java
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
```

#### SigninActivity.java
로그인 버튼을 누르면 존재하지 않는 아이디인지, 비밀번호를 틀렸는지에 대해 검사해 준다. 그리고 홈화면으로 돌아온다.
            
```java
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
```

#### SignupActivity.java
회원가입 버튼을 누르면 아이디 중복검사, 비밀번호 규칙, 전화번호 입력 규칙 등에 대한 Toast를 띄워준다. 해당 사항이 없다면 회원가입을 할 수 있도록 해두었고 데이터 베이스에 이를 저장한다. 또, 개인정보 약관 동의에 대한 약관 보기를 클릭하면 개인정보 약관을 AlertDialog에 담아 띄울 수 있도록 구현하였다.

```java
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

        String

 str = "1. 개인정보의 처리 목적 < 개인정보의 처리 목적 > \n" +
                " '당신'은 개인정보를 다음의 목적을 위해 처리합니다. 처리한 개인정보는 다음의 목적 이외의 용도로는 사용되지 않으며 이용 목적이 변경될 시에는 사전 동의를 구할 것입니다.\n" +
                " 가. 홈화면에서 보여줄 상품 리스트 및 상품 관련 정보를 제공하기 위해서 \n\n" +

                "2. 개인정보의 처리 및 보유 기간 < 개인정보의 처리 및 보유 기간 > \n" +
                " '당신'은 개인정보를 처리 및 보유 기간은 다음과 같습니다. (회원탈퇴 시에는 해당 정보가 바로 삭제되는 것을 보장합니다.)\n" +
                " 가. 홈화면에서 보여줄 상품 리스트 및 상품 관련 정보를 제공하기 위해서 : 회원탈퇴 시까지 \n\n" +

                "3. 개인정보의 제3자 제공에 관한 사항 < 개인정보의 제3자 제공에 관한 사항 > \n" +
                " '당신'은 개인정보를 제3자에게 제공하고 있지 않습니다. 개인정보를 제공할 경우에는 관련 법령에 따라 동의를 구할 것입니다. \n\n" +

                "4. 개인정보처리 위탁 < 개인정보처리 위탁 > \n" +
                " '당신'은 개인정보를 위탁하고 있지 않습니다. 개인정보 처리를 위탁할 경우에는 관련 법령에 따라 동의를 구할 것입니다. \n\n" +

                "5. 정보주체의 권리, 의무 및 그 행사방법 \n" +
                " 정보주체는 당신에 대해 언제든지 다음 각 호의 개인정보 보호 관련 권리를 행사할 수 있습니다.\n" +
                " 가. 개인정보 열람 요구 \n" +
                " 나. 오류 등이 있을 경우 정정 요구 \n" +
                " 다. 삭제요구 \n" +
                " 라. 처리정지 요구 \n\n" +

                "6. 개인정보의 파기 < 개인정보의 파기 > \n" +
                " '당신'은 개인정보를 다음의 기준에 따라 보존 및 이용 기간이 경과하거나 처리 목적 달성 시 지체없이 파기합니다. 단, 회원 탈퇴 시에는 해당 정보가 바로 삭제되는 것을 보장합니다.\n" +
                " 가. 홈화면에서 보여줄 상품 리스트 및 상품 관련 정보를 제공하기 위해서 : 회원탈퇴 시\n\n" +

                "7. 개인정보의 안정성 확보 조치 < 개인정보의 안정성 확보 조치 > \n" +
                " '당신'은 개인정보의 안정성 확보를 위해 다음과 같은 조치를 취하고 있습니다.\n" +
                " 가. 관리적 조치 : 내부관리계획 수립, 개인정보처리자 최소화 및 교육 실시\n" +
                " 나. 기술적 조치 : 개인정보처리 시스템 및 데이터베이스 암호화\n" +
                " 다. 물리적 조치 : 개인정보보호 장치(카메라 등) 설치\n" +
                " 라. 접속기록의 보관 및 위변조 방지 : 접속기록보관 시스템 설치 및 운영\n" +

                "8. 개인정보 보호책임자 작성 < 개인정보 보호책임자 작성 > \n" +
                " '당신'은 개인정보 보호 책임자를 다음과 같이 지정하고 있습니다.\n" +
                " 성명 : 송규원\n" +
                " 직책 : 대표\n" +
                " 전화번호 : 010-1234-5678\n" +
                " 이메일 : kws7599@gmail.com\n" +

                "9. 개인정보 처리방침 변경에 관한 사항 < 개인정보 처리방침 변경에 관한 사항 > \n" +
                " 이 개인정보처리방침은 시행일로부터 1일 이전부터 적용되며, 법령 및 방침에 따른 변경내용의 추가, 삭제 및 정정이 있을 시에는 변경사항의 시행일로부터 1일 이전부터 공지사항을 통하여 고지할 것입니다.";

        @Override
        public void onClick(View view) {
            AlertDialog.Builder builder = new AlertDialog.Builder(SignupActivity.this);
            builder.setTitle("개인정보 약관");
            builder.setMessage(str);
            builder.setNegativeButton("닫기", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialogInterface, int i) {
                    dialogInterface.cancel();
                }
            });
            builder.setPositiveButton("확인", new DialogInterface.OnClickListener() {
                @Override
                public void onClick(DialogInterface dialogInterface, int i) {
                    dialogInterface.cancel();
                }
            });
            AlertDialog alertDialog = builder.create();
            alertDialog.show();
        }
    });
}
```

### Fragment

#### HomeFragment.java
첫 화면이다. 동적 생성으로 5개의 상품을 나열한다. 

```java
public class HomeFragment extends Fragment {

    View view;
    String[] pname = new String[5];
    String[] pprice = new String[5];
    int[] pimage = new int[5];

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
       

 view = (View) inflater.inflate(R.layout.fragment_home, container, false);

        pname[0] = "Item 1";
        pname[1] = "Item 2";
        pname[2] = "Item 3";
        pname[3] = "Item 4";
        pname[4] = "Item 5";

        pprice[0] = "Price: 1000";
        pprice[1] = "Price: 2000";
        pprice[2] = "Price: 3000";
        pprice[3] = "Price: 4000";
        pprice[4] = "Price: 5000";

        pimage[0] = R.drawable.milk;
        pimage[1] = R.drawable.juice;
        pimage[2] = R.drawable.choco;
        pimage[3] = R.drawable.apple;
        pimage[4] = R.drawable.banana;

        LinearLayout productLinearLayout = view.findViewById(R.id.productLinearLayout);
        for (int i = 0; i < 5; i++) {
            LinearLayout linearLayout = new LinearLayout(getActivity());
            linearLayout.setOrientation(LinearLayout.HORIZONTAL);

            ImageView imageView = new ImageView(getActivity());
            imageView.setLayoutParams(new LinearLayout.LayoutParams(400, 400));
            imageView.setImageResource(pimage[i]);
            linearLayout.addView(imageView);

            TextView textView = new TextView(getActivity());
            textView.setLayoutParams(new LinearLayout.LayoutParams(ViewGroup.LayoutParams.WRAP_CONTENT, ViewGroup.LayoutParams.WRAP_CONTENT));
            textView.setPadding(20, 50, 20, 0);
            textView.setTextSize(30);
            textView.setText(pname[i] + "\n" + pprice[i]);
            linearLayout.addView(textView);

            productLinearLayout.addView(linearLayout);
        }

        return view;
    }
}
```

#### FavoriteFragment.java
두 번째 화면으로 첫 화면에서 선택한 상품을 나열한다.

```java
public class FavoriteFragment extends Fragment {

    View view;
    String[] pname = new String[5];
    String[] pprice = new String[5];
    int[] pimage = new int[5];

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        view = (View) inflater.inflate(R.layout.fragment_favorite, container, false);

        pname[0] = "Item 1";
        pname[1] = "Item 2";
        pname[2] = "Item 3";
        pname[3] = "Item 4";
        pname[4] = "Item 5";

        pprice[0] = "Price: 1000";
        pprice[1] = "Price: 2000";
        pprice[2] = "Price: 3000";
        pprice[3] = "Price: 4000";
        pprice[4] = "Price: 5000";

        pimage[0] = R.drawable.milk;
        pimage[1] = R.drawable.juice;
        pimage[2] = R.drawable.choco;
        pimage[3] = R.drawable.apple;
        pimage[4] = R.drawable.banana;

        LinearLayout productLinearLayout = view.findViewById(R.id.productLinearLayout2);
        for (int i = 0; i < 5; i++) {
            LinearLayout linearLayout = new LinearLayout(getActivity());
            linearLayout.setOrientation(LinearLayout.HORIZONTAL);

            ImageView imageView = new ImageView(getActivity());
            imageView.setLayoutParams(new LinearLayout.LayoutParams(400, 400));
            imageView.setImageResource(pimage[i]);
            linearLayout.addView(imageView);

            TextView textView = new TextView(getActivity());
            textView.setLayoutParams(new LinearLayout.LayoutParams(ViewGroup.LayoutParams.WRAP_CONTENT, ViewGroup.LayoutParams.WRAP_CONTENT));
            textView.setPadding(20, 50, 20, 0);
            textView.setTextSize(30);
            textView.setText(pname[i] + "\n" + pprice[i]);
            linearLayout.addView(textView);

            productLinearLayout.addView(linearLayout);
        }

        return view;
    }
}
```

### XML

#### activity_main.xml
`BottomNavigationView`를 이용한 3가지 액티비티 전환.

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <FrameLayout
        android:id="@+id/mainFramelayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@id/nav_view"
        android:layout_alignParentTop="true"
        android:layout_alignParentStart="true">

    </FrameLayout>

    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/nav_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:background="?android:attr/windowBackground"
        app:menu="@menu/bottom_nav_menu"
        android:backgroundTint="@color/black"
        app:itemIconTint="@color/white"
        app:itemTextColor="@color/white"
        app:layout_constraintTop_toTopOf="parent" />

</RelativeLayout>
```

#### bottom_nav_menu.xml
네비게이션의 item에 해당하는 메뉴의 XML이다.

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/homeId"
        android:icon="@drawable/ic_home"
        android:title="Home" />
    <item
        android:id="@+id/favoriteId"
        android:icon="@drawable/ic_favorite"
        android:title="Favorite" />
    <item
        android:id="@+id/userId"
        android:icon="@drawable/ic_person"
        android:title="User" />
</menu>
```

#### fragment_signin.xml
로그인 및 회원가입 버튼이 있는 화면.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SigninFragment">

    <Button
        android:id="@+id/toSignIn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="50dp"
        android:text="Sign In" />

    <Button
        android:id="@+id/toSignUp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="50dp"
        android:text="Sign Up" />

</LinearLayout>
```

#### fragment_favorite.xml
두 번째 화면이다. 선택한 상품을 나열한다.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout

_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".FavoriteFragment">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Favorite"
        android:textSize="50sp"
        android:layout_gravity="center_horizontal"/>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="1">
        <LinearLayout
            android:id="@+id/productLinearLayout2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">
        </LinearLayout>
    </ScrollView>

</LinearLayout>
```

#### fragment_home.xml
첫 번째 화면이다. 상품을 나열한다.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".HomeFragment">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Home"
        android:textSize="50sp"
        android:layout_gravity="center_horizontal"/>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="1">
        <LinearLayout
            android:id="@+id/productLinearLayout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">
        </LinearLayout>
    </ScrollView>

</LinearLayout>
```

#### activity_signup.xml
회원가입 화면이다. 아이디, 비밀번호, 이름, 휴대폰 번호, 주소를 입력할 수 있도록 구성되어 있다.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SignupActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Sign Up"
        android:textSize="50sp"
        android:layout_gravity="center_horizontal"/>

    <EditText
        android:id="@+id/et_id"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="50dp"
        android:hint="ID" />

    <EditText
        android:id="@+id/et_pw"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Password"
        android:inputType="textPassword" />

    <EditText
        android:id="@+id/et_name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Name" />

    <EditText
        android:id="@+id/et_hp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Phone"
        android:inputType="phone" />

    <EditText
        android:id="@+id/et_adress"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Address" />

    <Button
        android:id="@+id/btn_Join"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:text="Join"
        android:layout_gravity="center_horizontal"/>

    <Button
        android:id="@+id/btn_Tos"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:text="Terms of Service"
        android:layout_gravity="center_horizontal"/>

</LinearLayout>
```

#### activity_signin.xml
로그인 화면이다.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SigninActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Sign In"
        android:textSize="50sp"
        android:layout_gravity="center_horizontal"/>

    <EditText
        android:id="@+id/id_value"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="50dp"
        android:hint="ID" />

    <EditText
        android:id="@+id/pw_value"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Password"
        android:inputType="textPassword" />

    <Button
        android:id="@+id/btn_SignIn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:text="Sign In"
        android:layout_gravity="center_horizontal"/>

</LinearLayout>
```
