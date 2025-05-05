# Chapter 5. LifeCycle

---

<aside>
💡 **워크북 가이드라인**
1️⃣ 키워드 Essential은 자기주도학습!
2️⃣ 강의를 수강하고 나서 미션 수행하면서 트러블 슈팅 과정을 꼭! 정리해서 팀원들과 공유해보세요!
3️⃣ 주차별 Esssential은 권장이 아니라 필독입니다~
4️⃣ Essential에서 자세히 다루지 않은 내용은 레퍼런스 확인하셔서 살을 붙이시면 됩니다!

</aside>

---

---

## 📝 학습 목표

---

- Lifecycle이 왜 등장하였는지 이해하고, 어떤 것인지 설명할 수 있다.
- Activity의 Lifecycle에 대해 이해하고 설명할 수 있다.
- Fragment의 Lifecycle에 대해 이해한다.
- 각 Lifecycle을 적절하게 활용할 수 있다.
- SharedPreferences에 대해 이해하고 설명할 수 있다.

## ⚠️ 스터디 진행 방법

---

1. 스터디를 진행하기 전, 워크북 내용들을 모두 채우고 서로 모르는 내용들을 공유해주세요.
2. 미션을 모두 진행하시고 파트장 분께서 스터디원들의 코드 리뷰를 진행해주세요.
3. 다음주 스터디를 진행하기 전, 파트장의 간략한 설명을 듣고 개념의 윤곽을 잡아보세요.

## ✨ 파트장이 남기는 말

---

이번 주차에서 배우는 LifeCycle은 앱을 제대로 작동시키기 위해서 반드시 알아야 하는 개념입니다! 실제로 프로젝트를 진행할 때 LifeCycle을 이용해 기능을 구현할 때도 있고, LifeCycle을 고려하지 않아 기능이 제대로 작동하지 않는 경우도 발생할 수 있습니다.

LifeCycle의 개념이 중요하지 않은 것처럼 보일 수 있지만, 매우매우 중요한 개념이니 반드시 꼭!! 이해하고 넘어가 주시면 감사하겠습니다.

추가로 SharedPreferences 같은 경우도, 간단한 데이터 저장, 자동 로그인 등을 위해 자주 쓰이는 개념이니 모르는 부분이 있다면 꼭 정리하시고 넘어가시는 것을 추천드립니다.

이후에 RoomDB를 다루는 주차도 있으니, RoomDB와 SharedPreferences의 차이는 무엇인지 함께 공부하는 것도 매우 좋은 방법입니다.

## 🎯 키워드 Essential

---

<aside>
💡 주요 내용들에 대해 조사해보고, 자신만의 생각을 통해 정리해보세요!
강의와 레퍼런스를 참고하여 정의, 속성, 장단점 등을 적어주셔도 됩니다.
조사는 공식 홈페이지 **Best**, 블로그(최신 날짜) **Not Bad**

</aside>

- Lifecycle
    - Lifecycle이란 무엇일까요?
        - 앱의 구성요소(주로 Activity, Fragment, Service 등)가 생성되어 소멸되기까지의 일련의 상태 변화와 그에 따라 호출되는 메서드(콜백)를 의미한다.
        - 컴포넌트가 탄생(onCreate)해 성장(onStart, onResume)하고 일시정지(onPause, onStop)했다가 소멸(onDestroy)에 이르기까지의 과정을 체계적으로 관리하는 구조이다.
    - Lifecycle은 왜 등장하게 되었을까요?
        1. 자원 관리와 안정성
            - 모바일 환경에서는 메모리, 배터리 등 자원이 한정적이다. 사용자가 앱을 잠시 벗어나거나, 시스템이 메모리가 부족해 앱을 강제로 종료할 때, 적절히 자원을 해제하지 않으면 메모리 누수, 앱 크래시 등의 문제가 발생할 수 있다. Lifecycle을 도입함으로써 각 상태별로 자원을 할당/해제하는 시점을 명확히 구분 가능하다.
        2. 사용자 경험(UX) 향상
            - 앱이 예기치 않게 종료되거나, 사용자의 작업 내용이 사라지는 등의 문제를 방지하기 위해서 상태 변화에 따른 데이터를 저장하거 복원하는 처리가 필요하다.
        3. 코드의 유지보수성과 구조화
            - 초기 Android 앱 개발에서는 모든 상태 변화를 Activity/Fragment의 콜백에 직접 구현을 해야했기 때문에 코드가 복잡해지고, 여러 컴포넌트에서 동일한 동작을 반복적으로 구현하는 문제가 존재했다. Lifecycle 개념을 도입하여 각 컴포넌트가 자신의 상태 변화에 맞춰 동작을 자동으로 관리할 수 있도록 하였다.
        4. 안정적인 시스템 동작
            - Android OS는 여러 앱을 동시에 관리하며, 필요에 따라 앱의 프로세스를 중지하거나 재시작한다. Lifecycle은 이러한 시스템 동작에 맞춰 앱이 안정적으로 상태를 전환하고, 예측 가능한  동작을 하도록 보장한다.
    
    https://developer.android.com/topic/libraries/architecture/lifecycle?hl=ko
    
- Activity의 Lifecycle
    - Activity의 대표적인 Lifecycle은 어떤게 있을까요?
        - `onCreate()` : 컴포넌트가 처음 생성될 때 호출. 초기화 작업 수행
        - `onStart()` : 화면에 보이기 직전에 호출
        - `onResume()` : 사용자와 상호작용이 가능한 상태
        - `onPause()` : 다른 화면이 나타나기 직전, 일시정지 상태
        - `onStop()` : 화면에서 완전히 사라질 때 호출
        - `onDestroy()` : 컴포넌트가 완전히 소멸될 때 호출
        - `onRestart()` : 일시정지 또는 중단 상태에서 다시 시작될 때 호출
    - 각 Lifecycle을 활용하는 실제 예시들은 어떤게 있을까요?
        
        
        | **Lifecycle 메서드** | **활용 예시** |
        | --- | --- |
        | **`onCreate()`** | - 레이아웃 설정 (**`setContentView`**)
        - 변수 및 뷰 초기화
        - 데이터베이스/네트워크 연결 준비
        - savedInstanceState로 상태 복원 |
        | **`onStart()`** | - 애니메이션 시작
        - 위치 정보/센서 등 리스너 등록
        - UI에 필요한 데이터 로딩 시작 |
        | **`onResume()`** | - 카메라, 센서, GPS 등 리소스 활성화
        - 음악/비디오 재생 재개
        - UI 갱신(최신 데이터 반영) |
        | **`onPause()`** | - 변경된 데이터 저장(임시 저장)
        - 애니메이션/센서 일시 중지
        - 리소스 해제(카메라, 마이크 등) |
        | **`onStop()`** | - BroadcastReceiver 등 리스너 해제
        - 백그라운드 작업 중단
        - 데이터 영구 저장(DB, 파일 등) |
        | **`onRestart()`** | - 중단된 작업 재개
        - UI/데이터 재설정 |
        | **`onDestroy()`** | - 마지막 리소스 해제
        - 메모리 누수 방지
        - 서비스/스레드 종료 |
- MediaPlayer
    - MediaPlayer는 언제 사용할까요?
        - MediaPlayer는 안드로이드에서 오디오와 비디오 파일을 재생할 때 사용하는 기본 API이다.
        - 앱 내에 저장된 오디오/비디오 파일을 재생할 때
        - 파일 시스템에 있는 미디어 파일을 재생할 때
        - 인터넷을 통해 스트리밍되는 오디오나 비디오를 재생할 때
        - 다양한 미디어 소스를 통합하여 사용자에게 재생 기능을 제공할 때
    - MediaPlayer에서 사용할 수 있는 함수들은 무엇이 있으며, 어떤 기능을할까요? (ex create, pause, …)
        - create() : 앱 리소스에 있는 오디오 파일을 바로 재생할 수 있도록 준비
            
            ```kotlin
            MediaPlayer player = MediaPlayer.create(context, R.raw.sample_audio);
            ```
            
        - setDataSource(), prepare(), start() : 네트워크 스트리밍이나 외부 파일 재생에 사용
            
            ```kotlin
            player = new MediaPlayer();
            player.setDataSource(url); // URL 또는 파일 경로
            player.prepare();
            player.start();
            ```
            
        - pause(), seekTo(), start() : 일시정지 후 이어서 재생할 때 사용
            
            ```kotlin
            int position = player.getCurrentPosition();
            player.pause();
            player.seekTo(position);
            player.start();
            ```
            
        - stop(), reset(), release() : 재생을 중단하거나, 객체를 사용하거나, 리소르를 완전히 해제할 때 사용
            
            ```kotlin
            player.stop();
            player.reset();
            player.release();
            ```
            
        - isPlaying(), getCurrentPosition(), getDuration() : 현재 상태나 위치, 전체 길이 등을 확인할 때 사용
            
            ```kotlin
            if (player.isPlaying()) { ... }
            int pos = player.getCurrentPosition();
            int dur = player.getDuration();
            ```
            
    
- SharedPreferences
    - SharedPreference란 무엇일까요?
        - 안드로이드에서 기본적으로 제공하는 데이터 저장 방식이다.
        - 간단한 데이터를 Key-Value 쌍으로 저장할 수 있는 기능이다.
        - 주로 사용자 설정, 로그인 정보, 앱의 간단한 상태값 등의 소규모 데이터를 저장하는 데에 사용한다.
        - 내부적으로 xml 파일 형태로 저장되며, 앱 내에서 쉽게 값을 읽고 쓸 수 있도록 API를 제공한다.
    - SharedPreference는 어떤 방식으로 값을 저장할까요?
        - 위에서 언급한 것과 같이 Key-Value 형태로 xml 파일에 저장한다.
        - 동작 방식은 아래와 같다.
            - SharedPreference 객체를 생성하거나 가져온다.
            - SharedPreference.Editor를 통해 값을 추가하거나 수정한다.
            - `putString()`, `putInt()` 등 메서드로 값을 저장하고, `apply()` 또는 `commit()`을 호출하여 실제로 저장한다.
                - `apply()` : 권장하는 방법으로, 비동기적으로 저장한다.
                - `commit()` :  동기적으로 저장하며 메인 스레드 사용시에 주의해야한다.
            - 저장된 값은 앱이 삭제되거나 데이터가 초기화될 때까지 유지된다.
        - 값을 읽을 때는 `getString()`, `getInt()` 등으로 Key를 지정하여 값을 불러온다.
    - JSON과 GSON이란 무엇일까요?
        - JSON
            - JavaScript Object Notation의 약자로, 데이터를 저장하거나 네트워크로 주고받을 때 사용하는 가벼운 데이터 교환 포멧이다.
            - 구조는 Key-Value 쌍, 객체, 배열 등으로 구성되며 사람이 읽고 쓰기 쉽고 기계가 해석하기 쉽다는 장점이 있다.
                
                ```kotlin
                {
                  "name": "jisun",
                  "age": 25
                }
                ```
                
            - 다양한 언어에서 쉽게 파싱(해석)하고 생성할 수 있다.
        - GSON
            - google에서 개발한 Java용 라이브러리로, JSON과 Java 객체 간의 변환을 쉽게 처리할 수 있도록 해준다.
            - Java 객체를 JSON  문자열로 변환하거나, JSON 문자열을 Java 객체로 변환할 때 사용한다.
            - 별도의 복잡한 파싱 로직 없이 간단하게 객체와 JSON 간 변환이 가능하여, 서버와의 데이터 교환, 로컬 저장 등에 자주 활용된다.
            
            ```kotlin
            Gson gson = new Gson();
            String json = gson.toJson(myObject); // 객체 → JSON
            MyClass obj = gson.fromJson(jsonString, MyClass.class); // JSON → 객체
            ```
            

## 🕔 5주차 Essential

---

### Activity & Fragment LifeCycle

이전 챕터에서 간단하게 다루고 넘어갔었던 **Activity**에 대해서 더 자세히 알아보겠습니다.

앱 내에서 수많은 화면이 존재하고 각 화면 UI에 표시해줄 때 리소스(메모리 소모)가 들어가게 되고, 디바이스의 능력은 한정되어있습니다.

그래서 불필요하거나 쓰지 않는 **Activity**혹은 **Fragment**는 적절히 파괴하고 재활용을 할 경우 잠시 멈춰두었다가 필요할 때 다시 꺼내쓸 수도 있어야합니다.

![image.png](Chapter%205%20LifeCycle%201e2b57f4596b80e39264cfdd6aac69d5/image.png)

자료를 참고하시게 되면 **onCreate() → onStart → onResume() → onPause() → onStop() → onDestroy()** 순서로 **Activity**의 상태가 단계별로 세분화되어있는 것을 보실 수 있습니다.

[활동 수명 주기  |  Android Developers](https://developer.android.com/guide/components/activities/activity-lifecycle?hl=ko)

**Activity**와 **Fragment**의 생명주기가 다른 이유는 간단하게 말씀드리면 이전 챕터에서 다뤘던 것처럼 **Fragment**는 **Activity**의 하위에서 일종의 UI 파편이나 조각으로 존재하고 작동하기 때문입니다.

또한, **Fragment**는 재사용이 가능한 특성을 갖고 있기 때문에 **FragmentManager**를 통해서 추가, 교체가 이루어지기 때문에 **Activity**와 다른 생명주기를 갖고 있어야만 동작이 가능합니다. 

**FragmentManager**에 대한 설명은 그림 아래에서 이어나가도록 하겠습니다.

다시 말해서 **Fragment**는 **Activity** 하위, 종속되어있는 구조이기 때문에 당연히 **Activity**가 일시정지 상태가 된다면 **Fragment**도 그에 이어서 일시정지가 될 수밖에 없는 상태가 됩니다.

아래의 **Fragment**의 **LifeCycle**은 다음 그림과 같습니다.

![image.png](Chapter%205%20LifeCycle%201e2b57f4596b80e39264cfdd6aac69d5/image%201.png)

**FragmentManger**란 프래그먼트를 **add, replace, popbackstack**을 하는 상위 관리자 개념이라고 생각하시면 편합니다. 

또한, **Fragment**의 전반적인 생명주기를 감독하고 해당 **Fragment**의 상위 즉, **host** 역할을 맡고 있는 상위 **Activity**에 **Fragment**를 연결하고, **Fragment**가 더 이상 사용되지 않으면 분리하는 역할도 합니다.
 
여기서 주의할 점은 **Fragment** 생명주기는 **Activity**의 생명주기보다 먼저 앞서서 존재하는 것은 불가능합니다. 

위와 같은 상황을 방지하기 위해 XML 파일에 **<fragment>** 태그로 프래그먼트 대신 **<FragmentContainerView>** 를 추가하면 됩니다. 

이전 챕터의 예시 코드를 참고하시면 **<BottomNavigationView>** 태그가 작성되어있는 **XML** 코드에서 **ContainerView**가 선언되어있는 것을 보셨을 것입니다.
 

위 그림에서 한 가지 빠진 생명주기 단계가 있다면 **onAttach()**가 그것입니다. **Fragment**가 실행된 시점 이후의 생명주기를 다룬 것이기 때문에 없습니다.
 
**onAttach()**
**onAttach()**는 프래그먼트가 **FragementManager**에 추가되고, 상위 **Activity**에 연결될 때 호출됩니다. 위에서 말씀드렸다시피 이 시점부터가 진정으로 프래그먼트가 활성화됩니다.
 

**onCreate()**
문자 그대로 **Fragment**만 **CREATED**가 된 상황입니다.
이는 **FragmentManager**에 **add**가 되었을 때 도달하며 **onCreate()** 콜백 함수를 호출합니다.

중요한 점은 이 시점에는 아직 **Fragment View**가 생성되지 않았기 때문에 **Fragment**의 **View**와 관련된 작업을 수행하지 않도록 해야합니다.

**Fragment**를 생성하면서 넘겨준 값들이 있다면, 여기서 변수에 넣어주시면 됩니다.

```kotlin
class CalendarMyRecordFragment : Fragment(), OnMyDateClickListener {

    private var _binding: FragmentCalendarMyrecordBinding? = null
    private val binding: FragmentCalendarMyrecordBinding
        get() = requireNotNull(_binding){"FragmentCalendarMyrecordBinding -> null"}

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {

        _binding = FragmentCalendarMyrecordBinding.inflate(inflater, container, false)

        return binding.root
    }
}
```

**onCreateView()**
**Fragment**가 **View**를 그리기 위한, 즉 **Layout**을 **Inflate**하는 작업을 수행하는 부분입니다.

그래서 **UI**를 그려주고 **view binding**을 통해서 연결을 하기 위해서 **binding**을 선언한 것을 연결해주는 모습입니다.

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        navController = Navigation.findNavController(view)

        (requireActivity() as MainActivity).hideBottomNavigation(false)

        startCalendar.time = calendar.time

        // 월 달력
        binding.calendarViewPager.orientation = ViewPager2.ORIENTATION_HORIZONTAL
        binding.calendarViewPager.registerOnPageChangeCallback(object :
            ViewPager2.OnPageChangeCallback() {
            override fun onPageSelected(position: Int) {
                calendar.set(Calendar.MONTH, calendar.get(Calendar.MONTH) - 12 + position)
                updateCalendar()
            }
        })

        // 나의 기록 api 호출 후 정보 재가공
        myRecordViewModel.diaryCards.observe(viewLifecycleOwner) { diaryCards ->
            Timber.tag("CalendarFragment").d("DiaryCards loaded: $diaryCards")

            val imageMap = mapDiaryCardsToImages(diaryCards)
            updateCalendarWithImages(imageMap)
        }

        updateCalendar() // 초기 달력 업데이트
        dayTextView()
}
```

**onViewCreated()**
**onCreateView()** 를 통해 반환된 **View** 객체는 **onViewCreated()**의 파라미터로 다시 **savedInstanceState**와 함께 전달되는 것을 보실 수 있습니다.

이 시점부터는 **RecyclerView**의 **adapter**를 초기화시켜주거나 **ViewPager**의 **adapter**를 정의하거나 **viewmodel**을 **observing**을 해서 데이터 변화를 감지하는 등의 액션을 정의하는 곳입니다.
 
**onStart()**
**Fragment** 가 사용자에게 보여질 수 있을 때 호출됩니다.

**onResume()**
**Fragment**가 보이는 상태에서 모든 **Animation** 효과와 **Transition** 효과가 종료되고, **Fragment**가 사용자와 상호작용할 수 있을 때 **onResume()** 콜백이 호출됩니다. 
 
**onPause()**
사용자가 **Fragment**를 떠나기 시작했지만 **Fragment**는 여전히 **visible** 일 때 **onPause()**가 호출됩니다.

**Fragment**를 사용하는 이유를 엿볼 수 있는 것이 만약 회원가입하는 과정이었다면 사용자가 닉네임이나 상태를 잘못 선택해서 돌아가고 싶을 때 필요하게 됩니다.
 
 
**onStop()**
**Fragment** 가 더 이상 화면에 보이지 않게 되면 **Fragment**와 **View**의 **Lifecycle** 은 **CREATED** ``상태가 되고, **onStop()** 콜백 함수가 호출되게 됩니다.

```kotlin
override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
}
```

**onDestroyView()**

모든 **Animation** 효과와 **transition**이 완료되고, **Fragment**가 화면으로부터 벗어났을 경우 **Fragment View**의 **Lifecycle** 은 **DESTROYED** 상태가 되고 **onDestroy()**가 호출됩니다.

그리고 해당 시점에서는 불필요한 메모리 소모를 막기 위해서 **Fragment View**에 대한 모든 참조가 제거되어야 한다.

그래서 코드와 같이 처음에 **onCreateView**에서 참조했던 **binding**을 해제하기 위해 다시 **null** 값으로 정의하는 것을 확인할 수 있습니다.

**onDestroy()**
**Fragment**가 제거되거나 **FragmentManager**까지 완전히 파괴가 되었을 경우, 프래그먼트의 **Lifecycle** 은 **DESTROYED** 상태가 되고, **onDestroy()** 콜백 함수가 호출된다. 

해당 지점은 **Fragment Lifecycle**이 끝나게 되었다는 것을 알립니다.

그리고 **onAttach()**가 **onCreate()** 이전에 호출됐던 것처럼 **onDetach()** 또한 **onDestroy()** 이후에 호출되게 됩니다.

## 🔥 미션

---

## ✅ 5주차 미션 체크리스트

---

<aside>
💡 미션은 아래 내용을 확인해주세요!

- [ ]  [Song]화면 한곡재생 버튼 클릭 시 스레드 재시작 구현해보기 ‼️
- [ ]  [Main] 화면 Seekbar 구현해보기‼️
- [ ]  [Main] 화면 Seekbar 구현해서 [Song] 에서의 진행시간이 반영되도록 ‼️
    
    ![Untitled](Chapter%205%20LifeCycle%201e2b57f4596b80e39264cfdd6aac69d5/Untitled.png)
    
</aside>

## ❤️‍🔥 5주차 시니어 미션

---

<aside>
💡 실전미션을 통해 Demoday를 대비해보자!

- [ ]  **생명주기를 활용**하여 새 프로젝트를 생성하여 메모장 앱 만들어보기
    - [ ]  화면 구성
        - [ ]  메모 화면 (EditText와 다음 화면으로 넘어가는 Button)
        - [ ]  확인 화면 (TextView에 메모 화면에서 작성한 내용 보여주기)
    - [ ]  생명주기에 다음 기능 구현
        - [ ]  **onCreate** : Layout XML 파일을 Activity에서 ContentView로 사용할 수 있도록 하기 (즉, 화면 설정)
        - [ ]  **onResume** : onPause에서 저장한 전역변수 내용으로 EditText 내용으로 설정하기
            - [ ]  변수 값이 비어있다면 아무것도 안하기
        - [ ]  **onPause** : 현재까지 작성한 내용 Activity의 전역변수에 담아두기
        - [ ]  **onRestart** : Dialog를 활용하여 다시 작성할거냐고 묻는 창 띄우기
            - [ ]  다시 작성하지 않겠다고 하면 onPause에서 저장했던 변수 비우기
</aside>

## 📋 5주차 개발일지

---

<aside>
💡 미션 수행하신 내용을 아래에 정리해주세요!

</aside>

## ⚡ 트러블 슈팅

---

<aside>
💡 실습하면서 생긴 문제들에 대해서, **이슈 - 문제 - 해결** 순서로 작성해주세요.

</aside>

<aside>
💡

스스로 해결하기 어렵다면? 스터디원들에게 도움을 요청하거나 **너디너리의 지식IN 채널에 질문**해보세요!

</aside>

- ⚡이슈 No.1 (예시, 서식만 복사하시고 지워주세요.)
    
    **`이슈`**
    
    👉 앱 실행 중에 노래 다음 버튼을 누르니까 앱이 종료되었다.
    
    **`문제`**
    
    👉 노래클래스의 데이터리스트의 Size를 넘어서 NullPointException이 발생하여 앱이 종료된 것이었다. 
    
    **`해결`**
    
    👉  노래 다음 버튼을 눌렀을 때 데이터리스트의 Size를 검사해 Size보다 넘어가려고 하면 다음으로 넘어가는 메서드를 실행시키지 않고, 첫 노래로 돌아가게끔 해결
    
    **`참고레퍼런스`**
    
    [안드로이드 스튜디오 Render problem 해결방법 (레이아웃 XML 렌더링 에러, 문제, 오류)](https://wishml.tistory.com/53)
    

## 🤔 참고 자료

---

[https://www.youtube.com/watch?v=8hFFVGyMvcs](https://www.youtube.com/watch?v=8hFFVGyMvcs)

[https://www.youtube.com/watch?v=JzMIDiWcnok](https://www.youtube.com/watch?v=JzMIDiWcnok)

[https://www.youtube.com/watch?v=gYacRFMEPjk](https://www.youtube.com/watch?v=gYacRFMEPjk)

[https://www.youtube.com/watch?v=-2QPmS4OWos](https://www.youtube.com/watch?v=-2QPmS4OWos)

[https://www.youtube.com/watch?v=4rYMfpbpwPA](https://www.youtube.com/watch?v=4rYMfpbpwPA)

---

Copyright © 2025 Daemon(정승원) All rights reserved.