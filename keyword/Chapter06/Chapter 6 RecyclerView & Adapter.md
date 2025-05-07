# Chapter 6. RecyclerView & Adapter

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

- ListView가 무엇이고, 어느 때 사용하는 것인지 이해한다.
- ListView (RecyclerView)에서 Adapter가 어떤 역할을 하는지 이해하고, 활용할 수 있다.
- ListView의 한계점을 이해하고, RecyclerView가 ListView 대비 어떤 장점이 있는지 이해하고 활용할 수 있다.
- foreground/background service를 알고 사용할 수 있다.

## ⚠️ 스터디 진행 방법

---

1. 스터디를 진행하기 전, 워크북 내용들을 모두 채우고 서로 모르는 내용들을 공유해주세요.
2. 미션을 모두 진행하시고 파트장 분께서 스터디원들의 코드 리뷰를 진행해주세요.
3. 다음주 스터디를 진행하기 전, 파트장의 간략한 설명을 듣고 개념의 윤곽을 잡아보세요.

## ✨ 파트장이 남기는 말

---

<aside>
<img src="Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/HD-wallpaper-daemon-targaryen-house-of-the-dragon-season-1.jpg" alt="Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/HD-wallpaper-daemon-targaryen-house-of-the-dragon-season-1.jpg" width="40px" />

**RecyclerView는 사실상 모든 앱에 적용된다고 말할 수 있을만큼 가장 중요한 위젯이고 다른 위젯과는 달리 Adapter 개념이 추가되기 때문에 확실하게 공부해놓으시는 것을 추천드립니다!!**

또한 Adapter 등의 코드를 작성하실 때 한번 잘 작성해 두시면 좋은 템플릿을 얻는 것이니 잘 정리해 주시면 좋을 것 같습니다.

</aside>

한 번 공부하신 적이 있거나 쉽다고 느껴지시는 분들께서는 아래의 내용을 추가로 공부해 보시는 것을 추천해 드립니다.

- RecyclerView
    - drag - drop(item swap)
    - swipe(delete)
    - long click
    - item 동적 추가
- Foreground/Background Service
    - 해당 기능의 활용 방안 및 미션에서 다루지 않았던 기능 알아보기

## 🎯 키워드 Essential

---

<aside>
💡 키워드를 명확히 알고 있어야 기억이 더 뚜렷해지는 것 같아요. 자유롭게 서칭하면서 공부하고 본인의 언어로 가공시키면 남들에게 설명하는 것이 쉬워질거에요~
***공식 문서 강추!***

</aside>

- ListView
    - ListView란 무엇일까요?
        - 안드로이드에서 스크롤 가능한 항목을 표시할 수 있게 해주는 뷰(ViewGroup)이다.
        - 사용자가 여러 개의 데이터를 새로 방향으로 나열하여 확인하거나 선택할 수 있게 도와준다.
    - ListView에 들어갈 아이템들은 어떻게 저장해야 할까요?
        - 어댑터(Adpater)를 통해서 연결된다.
        - 아래의 코드처럼 저장할 수 있다.
        
        ```kotlin
        val listItems = arrayListOf("사과", "바나나", "체리")
        val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, listItems)
        listView.adapter = adapter
        ```
        
    - ListView는 어떤 구성요소로 되어있을까요?
        1. ListView 위젯
            - XML 레이아웃 또는 코드에서 정의하는 실제 목록 뷰이다.
            - `<ListView android:id="@+id/listView" ... />`
        2. Adpater
            - 데이터를 받아서 각 아이템에 맞는 뷰로 변환해주는 중개자 역할을 한다.
            - 종류 : `ArrayAdapter`, `BaseAdapter`, `CursorAdapter` 등
        3. Item 레이아웃
            - 각 항목이 화면에 어떻게 표시될지를 정의하는 XML
            - `simple_list_item_1`, `custom_item.xml` 등
        4. 데이터 소스
            - 어댑터에 전달되는 실제 데이터 (예 : 배열, 리스트, 데이터베이스 등)
    
    http://developer.android.com/reference/android/widget/ListView
    
- Adapter
    - Android에서 사용되는 Adapter란 무엇일까요?
        - 데이터 소스와 사용자 인터페이스를 연결하는 중간 매개체이다.
        - 데이터 항목들을 뷰 객체로 변환하여 ListView나 GridView 같은 ViewGroup에 전달하는 역할을 한다.
    - Adapter는 주로 어떤 역할을 할까요?
        1. 데이터 관리
        2. 각 항목 데이터에 대한 View 생성
        3. ListView 등 ViewGroup에 View를 제공
    - ListView의 Adapter는 어떤 구성 요소를 가지고 있을까요?
        1. 데이터 소스
        2. Context
        3. 레이아웃 리소스
        4. getView() 리소스
        5. 뷰 홀더 패턴 ← 옵션
- RecyclerView
    - RecyclerView란 무엇일까요?
        - 안드로이드에서 목록이나 그리드 형태의 데이터를 효율적으로 표시하기 위한 향상된 ViewGroup이다.
        - ListView의 개선된 버전으로, 아이템의 뷰 재사용(recycling)과 유연한 레이아웃 관리를 지원한다.
        - 다양한 레이아웃 매니저와 애니메이션, 뷰 타입 등을 손쉽게 사용할 수 있게 설계되어 있다.
    - RecyclerView와 ListView는 어떤 차이점이 있을까요?
        
        
        | 구분 | RecyclerView | ListView |
        | --- | --- | --- |
        | 뷰 재사용 | ViewHolder 강제 적용 | ViewHolder 선택적 적용 |
        | 레이아웃 지원 | Linear, Grid, Staggered 등 유연함 | 기본 세로 리스트만 지원 |
        | 아이템 애니메이션 | 기본 제공 (삽입, 삭제, 이동) | 직접 구현해야 함 |
        | 커스터마이징 | 아이템 드래그/스와이프 등 확장 쉬움 | 커스터마이징 어려움 |
        | 성능 | 더 뛰어남 (뷰 바인딩, 애니메이션 등) | 상대적으로 단순하고 제한적 |
    - RecyclerView Adapter는 어떤 구성 요소를 가지고 있을까요?
        1. 데이터 소스
        2. ViewHolder 클래스
        : 아이템 뷰의 참조를 저장하는 클래스. findViewById 호출을 줄여서 성능을 향상시킨다.
        3. onCreateViewHolder()
        : 새로운 ViewHolder 객체를 생성하고 레이아웃을 inflate 한다.
        4. onBindViewHolder()
        : ViewHolder에 데이터를 바인딩한다.
        5. getItemCount()
        : 데이터 항목 수 반환
        
        예시 코드
        
        ```kotlin
        class MyAdapter(private val items: List<String>) :
            RecyclerView.Adapter<MyAdapter.MyViewHolder>() {
        
            class MyViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
                val textView: TextView = itemView.findViewById(R.id.my_text_view)
            }
        
            override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyViewHolder {
                val view = LayoutInflater.from(parent.context)
                    .inflate(R.layout.item_layout, parent, false)
                return MyViewHolder(view)
            }
        
            override fun onBindViewHolder(holder: MyViewHolder, position: Int) {
                holder.textView.text = items[position]
            }
        
            override fun getItemCount(): Int = items.size
        }
        ```
        
    - RecyclerView를 설정할 때 주의해야 하는 점은 무엇이 있을까요?
        1. LayoutManager 설정을 반드시 해야한다.
        2. ViewHolder를 올바르게 구현해야 한다.
        3. 데이터 변경 시 notify 메서드를 적절히 호출해야한다.
        4. 아이템 클릭 이벤트는 ViewHolder 또는 Adapter 내에서 처리해야 한다.
        5. 성능 최적화를 위해 DiffUtil 사용을 고려한다.
    - ViewPager2 에서 사용했던 FragmentStateAdapter와 RecyclerView.Adapter는 어떤 차이가 있을까요?
        
        
        | 항목 | FragmentStateAdapter | RecyclerView.Adapter |
        | --- | --- | --- |
        | 용도 | ViewPager2에서 Fragment를 페이지로 표시할 때 사용 | RecyclerView에서 일반 아이템 View를 표시할 때 사용 |
        | 바인딩 대상 | Fragment | View (레이아웃 XML) |
        | 생명주기 | FragmentManager를 사용하며 Fragment 생명주기 관리가 필요하다 | 일반 View이며 생명주기 관리가 필요 없다 |
        | 주요 메서드 | `createFragment(position: Int)` | `onCreateViewHolder()`, `onBindViewHolder()` |
        | 내부 구조 | Fragment를 메모리에 보관하거나 파괴해 상태를 유지 | ViewHolder를 재사용하면서 화면에 표시 |
- foreground service
    - foreground service란 무엇일까요?
        - 사용자에게 명확하게 인식되면서 실행되는 서비스이다.
        - 일반적인 백그라운드 서비스와 달리, foreground service는 시스템 자원이 부족할 때에도 강제로 종료되지 않고 우선순위가 높다.
        - 실행 중임을 사용자에게 알리기 위해 항상 알림(Notification)을 표시해야 한다.
    - foreground service를 사용하는 이유는 무엇일까요?
        - 음악재생 / 피트니스 앱의 운동 추적 / 파일 다운로드 또는 업로드 / 네비게이션 앱에서 위치 추적 / VoIP 앱의 전화 통화 유지 등의 사용자 인식이 중요한 작업을 위해 사용된다.
    - foreground service 사용 시 주의사항은 무엇이 있을까요?
        1. **Notification 필수**
            
            Foreground Service를 시작할 때 `startForeground()`를 호출하고, 사용자에게 보여줄 **지속적인 알림**을 반드시 제공해야 한다. 알림이 없으면 시스템이 앱을 종료시킬 수 있다.
            
        2. **권한 요청 필요** (`Android 9 이상`)
            
            `FOREGROUND_SERVICE` 권한을 AndroidManifest.xml에 선언해야 한다:
            
            ```xml
            xml
            복사편집
            <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
            ```
            
        3. **Android 10(Q) 이상에서는 백그라운드에서 startForegroundService() 호출 시 제한**
            
            서비스는 일정 시간 안에 `startForeground()`를 호출해야 하며, 그렇지 않으면 시스템이 앱을 종료한다.
            
        4. **배터리 최적화 대상이 될 수 있음**
            
            장시간 실행되는 서비스는 배터리 소모가 크므로 꼭 필요한 작업에만 사용해야 한다.
            
        5. **사용자에게 방해되지 않도록 알림 채널 구성 고려**
            
            알림의 중요도 설정과 채널 이름을 명확히 설정하여 사용자 경험을 해치지 않도록 해야 한다.
            
- background service
    - background service란 무엇일까요?
        - 사용자 인터페이스(UI)와 직접적인 상호작용 없이, 앱이 화면에 표시되지 않아도 백그라운드에서 실행되는 서비스이다.
        - 앱이 종료된 상태에서도 데이터를 동기화하거나 알림을 예약하는 등의 작업을 수행할 수 있다.
    - background service를 사용하는 이유는 무엇일까요?
        - 서버로부터 주기적으로 데이터 동기화
        - 알림 예약 처리
        - 로컬 DB 정리 또는 캐시 관리
        - 사용자가 앱을 떠난 이후에도 이어져야 하는 작업
    - background service 사용 시 주의사항은 무엇이 있을까요?
        - **Android 8.0 이상에서는 제약이 크다**
            
            앱이 백그라운드 상태일 때는 `startService()`로 바로 실행할 수 없고, `startForegroundService()`로 전환하거나 WorkManager 등을 사용해야 한다.
            
        - **배터리 사용 최적화를 고려해야 한다**
            
            백그라운드에서 장시간 실행되는 서비스는 배터리를 과도하게 소모할 수 있으므로 제한적으로 사용해야 한다.
            
        - **백그라운드 실행 제한 정책 적용 대상이다**
            
            Doze 모드나 앱 대기 상태(App Standby)에 따라 서비스가 중단되거나 지연될 수 있다.
            
        - **브로드캐스트 리시버에서 서비스 시작 시 제한됨**
            
            Android 8.0부터는 암시적 브로드캐스트를 통해 서비스 시작이 불가능하고, 명시적 호출 또는 WorkManager 사용이 권장된다.
            
        - **대체 기술 고려**
            
            주기적인 작업 → `WorkManager`
            
            단기 작업 → `JobIntentService`
            
            장시간 실행 → `ForegroundService`
            

## 🕕 6주차 Essential

---

# ListView & RecyclerView

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image.png)

**Fragment**가 **Activity**를 보완하기 위해 등장한 것처럼, **RecyclerView** 이전에는 **ListView**라는 개념이 존재했습니다.

**RecyclerView**의 특징과 사용 방식에 대해 먼저 설명해보겠습니다.

**Adapter**에 대해 언급하자면, 일반적으로 노트북 충전기 어댑터처럼 항상 필요한 구성품이라고 볼 수 있습니다. **RecyclerView**의 각 **item**은 **adapter**를 통해 **View**와 연결되어 표시됩니다.

# **RecyclerView 구성 요소**

**RecyclerView**의 대표적인 구성 요소로는 **Adapter**, **LayoutManager**, **ViewHolder**가 존재합니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%201.png)

## Adapter

각각의 아이템에 들어갈 데이터와 **RecyclerView**를 연결해주는 매개체라고 보시면 됩니다. 

또한, 본인이 직접 **Adapter** 클래스를 생성한 다음에 연결해주어야하고 
안드로이드 라이브러리에 내장되어있는 **RecyclerView.Adapter**를 상속받아서 
총 3개의 메서드를 **override**합니다. 

**getItemCount**

→ 전체 item 개수를 리턴

**onCreateViewHolder**

→ ViewHolder 생성

**onBindViewHolder**

→ 생성된 **ViewHolder**에 실제 데이터를 **binding**해줍니다.

→ 인자로 **ViewHolder**와 **position**을 받아서 holder의 데이터를 변경시킵니다.

→ Adapter 작동 순서는 **getItemCount → onCreateViewHolder → onBindViewHolder** 입니다.

## ViewHolder

**Adapter**는 생성한 뷰를 저장하고 관리하는 객체입니다. 

스크롤을 해서 위로 올라가면 화면 밖으로 나간 **View**는 다시 재활용해야 하기 때문에 어떤 **View**가 올라갔는지 지속적으로 추적할 필요가 있습니다. 

이 부분은 **ViewHolder**가 담당하여, 화면에 표시된 **View**의 상태를 기억하고 관리합니다.

## LayoutManager

목록 아이템들이 2열로 나열할지, 1열로 나열할지 그 형태를 관리하며, 
목록이 가로 방향이나 세로 방향으로 스크롤될지도 결정하는 역할을 합니다.

즉, 말 그대로 아이템의 **레이아웃**을 관리하는 것이죠. 이 작업은 **LayoutManager**가 담당합니다.

**LayoutManager**는 **RecyclerView**의 레이아웃 방향과 아이템 배치를 조정합니다.

- **LinearLayoutManager** : 
수평 또는 수직 방향, 일렬로 아이템 뷰 배치
- **GridLayoutManager** : 
바둑판 모양으로 배치(여기서부터 격자 배열이 가능해짐)
- **StaggeredGridLayoutManager**: 
GridLayout과 그 뿌리가 같지만 배열이 불규칙적 
(구글 이미지 검색이나 핀터레스트 사진 목록이 그 예시)

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%202.png)

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%203.png)

도식화가 되어있는 그림부터 헷갈리니까 에스컬레이터를 상상해봅시다. 

에스컬레이터에서 사람이 나올 때 마지막으로 밟아서 넘어가는 칸들은 밑으로 내려갔다가 다시 처음 시작하는 칸으로 넘어오죠?

**공통점은 재활용입니다.**

# ListView X → RecyclerView O

**Adapter**는 **ViewHolder**를 통해 처음 화면에 보이는 뷰 객체를 **hold**하고 있어야 합니다.

**ListView**는 사용자가 아이템 목록을 스크롤할 때마다 화면 밖으로 사라지는 뷰를 삭제하고, 새롭게 등장하는 아이템을 계속 생성하므로 **cost가 매우 높습니다.**

반면, **RecyclerView**는 아이템이 100개, 1000개가 넘어가도 사용자의 화면에 보이는 **View**만 생성합니다. 
스크롤 시, 화면 밖으로 사라지는 아이템은 재사용을 위해 가장 아래쪽 아이템으로 이동시켜 객체를 재활용합니다.

이를 이해하기 쉽게 예시로 설명하면, 화면에 100개의 아이템을 표시해야 할 때 다음과 같습니다.

- **ListView**는 스크롤 중에 100번에 걸쳐 아이템을 삭제하고 새로 생성하는 과정을 반복합니다.
- **RecyclerView**는 10개 정도만 만들어 놓고 이 10개를 계속해서 재활용합니다. 
즉, 스크롤하면서 새롭게 나타나는 아이템과 더 이상 필요 없는 아이템을 재사용하며, 
데이터만 바인딩하여 View 객체를 재활용합니다.

결국, **ListView**는 화면에 표시할 아이템의 개수만큼 뷰를 생성하므로 메모리 사용과 처리 비용이 효율적입니다. 또한, **RecyclerView**는 **LayoutManager**를 통해 몇 개짜리 열로 배치할지, 스크롤 방향을 사전에 정의할 수 있지만, **ListView**는 수직 스크롤만 가능합니다.

# RecyclerView 실제 작동 방식

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%204.png)

하나의 화면에 item 1부터 item 5가 있다고 가정해봅시다.

item x는 화면을 위로 스크롤할 때 새롭게 나타날 아이템입니다.

**Step 1. 처음 시작될 때 item x부터 item 4까지 화면에 표시됩니다.** 

item 5는 아래로 스크롤할 경우 새롭게 나타날 아이템입니다. 

첫 화면에 보여지는 item들을 visible view라고 하겠습니다.

**Step2. 아래 방향으로 스크롤하면 item x는 위로 올라가고 item 5가 visible view에 포함이 됩니다.**

item 6는 waiting view가 되고 item x는 화면 밖을 벗어나서 scrapped view가 됩니다. 

여기서 ScrapView는 RecyclerView에서 visible 상태였다가 

invisible 상태로 바뀌게 된 뷰를 의미합니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%205.png)

**Step3. 한 단계를 더 스크롤하면 item 1은 item x와 같이 scrapped view에 포함되어 scrapped views collection이 구성됩니다.** 

이제, item 7이 올라올 차례일 때 scrapped views collection에 있었던 view가 사용됩니다.

**Step4. 이 때 재사용된 view들을 dirty view라고 해보겠습니다.** 

dirty view들을 사용하게 되면서 RecyclerView Adapter로 인해 리바운드가 발생하게 됩니다.

여기서 리바운드란 농구에서 공이 한 번 더 튕기는 것을 말하는데 여기서도 비슷하게 적용됩니다.

한 번 사용이 되었던 view들이 또 다시 사용된다는 의미에서 리바운드라고 표현했습니다.

여기까지 **RecyclerView**가 어떤 방식으로 동작하는지 자세히 살펴보았고 
**RecyclerView**의 아이템 재사용성이 얼마나 효율적인지 알 수 있을 것 같습니다.

이제 코드를 살펴보겠습니다.

# RecyclerView 활용 방법 with code

이전 챕터에서 실습을 진행하셨다면 **view binding**에 대해서 공부를 해보셨을텐데요

마찬가지로 **RecyclerView**에서도 **binding**을 통해서 손쉽게 생성할 수 있습니다.

**Gradle Scripts>build.gradle.kts(Module 단위)** 위치에서 다음과 같이 **ViewBinding**을 사용합니다.

```kotlin
android {
		// 중략...
		
    buildFeatures {
        viewBinding = true
    }
}
```

RecyclerView를 만들 때는 필자는 이러한 순서로 진행합니다.

<aside>
⌛

1. RecyclerView가 들어갈 XML Layout 작성
2. RecyclerView에 item으로 들어갈 XML Layout 작성
3. RecyclerView Adapter 클래스 작성
4. 필요하다면 ClickListener 작성
5. RecyclerView가 들어갈 화면의 Fragment or Activity 클래스에서 
해당 RecyclerView 및 Adapter 초기화 코드 작성
</aside>

우선, **XML Layout**을 작성해보겠습니다.

## fragment_notice.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
		xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/background_white">

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline_notice_h"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_begin="53dp" />

    <LinearLayout
        android:id="@+id/notice_back_layout"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_marginStart="17dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <ImageView
            android:id="@+id/notice_back_btn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="15dp"
            android:src="@drawable/back_button" />

    </LinearLayout>

    <TextView
        android:id="@+id/notice_title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/notice"
        android:textColor="@color/black"
        style="@style/sc_r15"
        android:layout_marginStart="25dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/guideline_notice_h" />

		// RecyclerView
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/notice_rv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/notice_title" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

**fragment_notice.xml**에 작성되어있는 **RecyclerView** 위젯만 보시면 됩니다.

item list에 들어갈 아이템 레이아웃의 종류가 1가지밖에 없다면 XML에서 **listitem**속성으로 지정할 수 있습니다. 

종류가 2가지 이상이 들어간다면 **Adapter**에서 따로 설정을 해야하기 때문에 사용하지 않았지만 여러분들은 각자 상황에 맞게 사용하시면 될 것 같습니다.

완성된 화면은 다음과 같습니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%206.png)

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%207.png)

## item_notice_card_check.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout 
		xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <data>
        <variable
            name="item_card_check"
            type="com.toyou.toyouandroid.model.NoticeItem.NoticeCardCheckItem" />
    </data>

    <FrameLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="20dp">

        <LinearLayout
            android:layout_width="340dp"
            android:layout_height="60dp"
            android:weightSum="5">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"/>

            <androidx.constraintlayout.widget.ConstraintLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="4">
                <ImageView
                    android:id="@+id/notice_card_check_delete"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:src="@drawable/notice_delete_ic"
                    android:background="@color/transparent"
                    app:layout_constraintStart_toStartOf="parent"
                    app:layout_constraintEnd_toEndOf="parent"
                    app:layout_constraintTop_toTopOf="parent"
                    app:layout_constraintBottom_toBottomOf="parent"/>
            </androidx.constraintlayout.widget.ConstraintLayout>
        </LinearLayout>

        <androidx.constraintlayout.widget.ConstraintLayout
            android:id="@+id/notice_layout"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/notice_mypage_box">

            <TextView
                android:id="@+id/notice_box"
                android:layout_width="340dp"
                android:layout_height="60dp"
                android:text="@{String.format(@string/notice_card_check, item_card_check.nickname)}"
                android:textColor="@color/black"
                style="@style/sc_r10"
                android:gravity="center_vertical"
                android:paddingStart="17dp"
                android:paddingEnd="0dp"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <androidx.appcompat.widget.AppCompatButton
                android:id="@+id/notice_next_btn"
                android:layout_width="24dp"
                android:layout_height="24dp"
                android:background="@drawable/social_arrow"
                android:layout_marginEnd="16dp"
                app:layout_constraintEnd_toEndOf="@+id/notice_box"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintBottom_toBottomOf="parent"/>
        </androidx.constraintlayout.widget.ConstraintLayout>

    </FrameLayout>
</layout>
```

알림 화면에 들어갈 **item**을 커스텀해서 작성하고 

필자 같은 경우에 알림 메시지에 클릭할 수 있는 버튼이 존재해야하고 아이템을 목록에서 스와이프해서 삭제하는 기능까지 있어서 Layout이 중첩으로 들어가있습니다. 

**통상적으로 RecyclerView에 들어가는 item xml 파일이름은 item_으로 시작합니다.**

## NoticeAdapter.kt

```kotlin
class NoticeAdapter(
    private val items: MutableList<NoticeItem>,
    private val viewModel: NoticeViewModel,
    private val listener: NoticeAdapterListener
    ) : RecyclerView.Adapter<RecyclerView.ViewHolder>() {
}
```

**NoticeAdapter**클래스를 만들고 **RecyclerView.Adapter**를 상속받고 <> 안에는 **view holder**를 넣어줘야합니다.

```kotlin
sealed class NoticeItem(open val alarmId: Int) {
    data class NoticeFriendRequestItem(val nickname: String, override val alarmId: Int) : NoticeItem(alarmId)
    data class NoticeFriendRequestAcceptedItem(val nickname: String, override val alarmId: Int) : NoticeItem(alarmId)
    data class NoticeCardCheckItem(val nickname: String, override val alarmId: Int) : NoticeItem(alarmId)
}
```

**Adapter**에 들어갈 **item**은 기존에 선언해두었던 **NoticeItem data class**로 정의합니다.

API 호출을 통해서 받아온 정보이므로 변동성 때문에 **MutableList**로 설정해두었습니다. 

실습을 할 때에는 수동으로 정보를 직접 넣어주기 때문에
**ArrayList**로 받으셔서 **Activity**나 **Fragment**에서 **Adapter**를 초기화시킬 때 데이터를 넣으시면 됩니다.

```kotlin
val datas = mutableListOf(
		data("이름", "멘트", R.drawable.image)
		data("이름", "멘트", R.drawable.image)
		data("이름", "멘트", R.drawable.image)
)
```

나중에 이런 식으로 **Activity**나 **Fragment**에서 더미 데이터를 만들어서 
**Adapter**를 초기화할 때 인자값으로 **datas**를 그대로 넣어주기만 하면 됩니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%208.png)

만약에 처음 **RecyclerView**를 구현하실 때 메서드를 일일이 **override**할 필요없이 
**Implement members**를 하면 한꺼번에 자동으로 입력할 수 있습니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%209.png)

이처럼 **Implement members**를 할 경우 
**RecyclerView.Adapter**에 필수적으로 구현되어야할 메서드를 자동으로 추가할 수 있습니다.

```kotlin
override fun getItemCount(): Int = items.size
```

필수적으로 구현해야할 메서드 중 **getItemCount()**에서는 
아이템이 총 몇 개로 구성되어있는지 알려줘야하기 때문에 **items.size**를 반환합니다.

```kotlin
override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder {
        return when (viewType) {
            TYPE_CARD_CHECK -> {
                val binding = DataBindingUtil.inflate<ItemNoticeCardCheckBinding>(
                    LayoutInflater.from(parent.context),
                    R.layout.item_notice_card_check,
                    parent,
                    false
                )
                CardCheckViewHolder(binding)
            }
            
            // when 구문에 들어가는 다른 인자값에 따른 코드는 중략...
            
            else -> throw IllegalArgumentException("유효하지 않은 NoticeAdapter type입니다.")
        }
}
```

현재 필자는 코드에 **data binding**을 사용하고 있지만 **view binding**을 사용해도 무방하므로 코드를 변경하면 다음과 같습니다. 

목록에 들어갈 아이템 종류가 3가지나 되기 때문에 **when** 구문을 통해서 **viewType**으로 **binding**을 달리 했었는데 아이템 종류가 1가지인 경우에는 아래와 같이 작성하게 됩니다.

```kotlin
override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder {
				val binding = ItemNoticeCardCheckBinding.inflate(
                    LayoutInflater.from(parent.context),
                    R.layout.item_notice_card_check,
                    parent,
                    false
                )
		    return CardCheckViewHolder(binding)
}
```

여기서 반환한 **view holder** 객체는 자동으로 **onBindViewHolder()**함수의 매개변수로 전달됩니다.

**xml** 파일을 **inflate**해야 코드로 변환해서 사용할 수 있는데 **LayoutInflater**가 그 역할을 수행합니다.

**화면의 무수한 view들 중에서 메모리가 RecyclerView를 인식하고서 item을 넣어주려면 
부모 view의 context를 참조해야하므로 .from으로 가져오는 것도 확인할 수 있습니다.**

**RecyclerView**는 화면에 보여지는 **view holder**를 생성하고 화면에 보여지지 않는 부분은 재활용해야하기 때문에 화면에 보여지는 갯수까지만 호출되어야합니다.

![image.png](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image%204.png)

```kotlin
inner class CardCheckViewHolder(private val binding: ItemNoticeCardCheckBinding) : RecyclerView.ViewHolder(binding.root) {
        fun bind(item: NoticeItem.NoticeCardCheckItem) {
            binding.itemCardCheck = item
            binding.noticeCardCheckDelete.setOnClickListener {
                // 삭제 API 호출
                viewModel.deleteNotice(item.alarmId, this.layoutPosition)
                removeItem(this.layoutPosition)
            }

            binding.noticeLayout.setOnClickListener {
                // 알림 메시지 클릭 후 메시지 삭제
                listener.onFriendCardItemClick(item)
                viewModel.deleteNotice(item.alarmId, this.layoutPosition)
                removeItem(this.layoutPosition)
            }

            binding.executePendingBindings()
        }
    }
```

**inner class**로 h**older** 클래스를 만들고 생성자로는 처음 빌드파일에서 선언했던 **viewBinding**을 사용해서 넣습니다. 

**item xml 파일을 생성을 먼저 한 이유도 여기에 있습니다.**

파일이 생성된 뒤에 **binding**을 넣을 수 있기 때문에 **ItemNoticeCardCheckBinding**으로 **item**에 접근할 수 있게 됩니다.

## Adapter 전체 예시 코드

```kotlin
class NoticeAdapter(
    private val items: MutableList<NoticeItem>,
    private val viewModel: NoticeViewModel,
    private val listener: NoticeAdapterListener
    ) : RecyclerView.Adapter<RecyclerView.ViewHolder>() {
    
    companion object {
        private const val TYPE_FRIEND_REQUEST = 1
        private const val TYPE_CARD_CHECK = 2
        private const val TYPE_FRIEND_REQUEST_ACCEPTED = 3
    }

    override fun getItemViewType(position: Int): Int {
        return when (items[position]) {
            is NoticeItem.NoticeFriendRequestItem -> TYPE_FRIEND_REQUEST
            is NoticeItem.NoticeFriendRequestAcceptedItem -> TYPE_FRIEND_REQUEST_ACCEPTED
            is NoticeItem.NoticeCardCheckItem -> TYPE_CARD_CHECK
        }
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder {
        return when (viewType) {
            TYPE_CARD_CHECK -> {
                val binding = DataBindingUtil.inflate<ItemNoticeCardCheckBinding>(
                    LayoutInflater.from(parent.context),
                    R.layout.item_notice_card_check,
                    parent,
                    false
                )
                CardCheckViewHolder(binding)
            }
            
            // when 구문에 들어가는 다른 인자값에 따른 코드는 중략...
            
            else -> throw IllegalArgumentException("유효하지 않은 NoticeAdapter type입니다.")
        }
    }

    override fun onBindViewHolder(holder: RecyclerView.ViewHolder, position: Int) {
        when (holder) {
            is FriendRequestViewHolder -> holder.bind(items[position] as NoticeItem.NoticeFriendRequestItem)
            is FriendRequestAcceptedViewHolder -> holder.bind(items[position] as NoticeItem.NoticeFriendRequestAcceptedItem)
            is CardCheckViewHolder -> holder.bind(items[position] as NoticeItem.NoticeCardCheckItem)
        }
    }

    override fun getItemCount(): Int = items.size

		// 다른 ViewHolder 중략...

    inner class CardCheckViewHolder(private val binding: ItemNoticeCardCheckBinding) : RecyclerView.ViewHolder(binding.root) {
        fun bind(item: NoticeItem.NoticeCardCheckItem) {
            binding.itemCardCheck = item
            binding.noticeCardCheckDelete.setOnClickListener {
                // 삭제 API 호출
                viewModel.deleteNotice(item.alarmId, this.layoutPosition)
                removeItem(this.layoutPosition)
            }

            binding.noticeLayout.setOnClickListener {
                // 알림 메시지 클릭 후 메시지 삭제
                listener.onFriendCardItemClick(item)
                viewModel.deleteNotice(item.alarmId, this.layoutPosition)
                removeItem(this.layoutPosition)
            }

            binding.executePendingBindings()
        }
    }

    fun removeItem(position: Int) {
        if (position >= 0 && position < items.size) {
            items.removeAt(position)
            notifyItemRemoved(position)
            notifyItemRangeChanged(position, items.size) // 아이템을 제거한 이후의 아이템들에 대해 포지션 업데이트
        }
    }
}

```

## AdapterListener

```kotlin
interface NoticeAdapterListener {
    fun onDeleteNotice(alarmId: Int, position: Int)
    fun onShowDialog()
    fun onFriendRequestApprove(name: String)
    fun onFriendRequestItemClick(item: NoticeItem.NoticeFriendRequestItem)
    fun onFriendRequestAcceptedItemClick(item: NoticeItem.NoticeFriendRequestAcceptedItem)
    fun onFriendCardItemClick(item: NoticeItem.NoticeCardCheckItem)
}
```

**ListView**에서는 **clickListener**가 내장되어있지만 **RecyclerView**에서는 그렇지 않기 때문에 직접 **NoticeAdapterListener interface**를 구현해서 연결해야합니다.

## Fragment(Activity)

```kotlin
class NoticeFragment : Fragment(), NoticeAdapterListener {}
```

연결할 **Adapter**에 **Listener**를 연결해준 모습입니다.

```kotlin
private lateinit var listener: NoticeAdapterListener
private lateinit var noticeAdapter: NoticeAdapter
```

**listener**와 **adpater**를 초기화시킵니다.

```kotlin
private fun setupRecyclerView(items: List<NoticeItem>) {
        val adapter = NoticeAdapter(items.toMutableList(), viewModel, listener)
        binding.noticeRv.layoutManager = GridLayoutManager(context, 1)
        binding.noticeRv.adapter = adapter

        val swipeToDeleteNotice = SwipeToDeleteNotice().apply {
            setClamp(resources.displayMetrics.widthPixels.toFloat() / 5)
        }
        ItemTouchHelper(swipeToDeleteNotice).attachToRecyclerView(binding.noticeRv)

        binding.noticeRv.apply {
            setOnTouchListener { v, _ ->
                swipeToDeleteNotice.removePreviousClamp(this)
                v.performClick()
                invalidateItemDecorations()
                false
            }

            setOnClickListener {
            }
        }
}
```

필자는 **adapter**를 설정하는 부분을 함수로 분리한 다음에 작성했습니다.

알림 목록에 스와이프 기능을 넣는 관계로 **ItemTouchHelper**와 **setOnTouchListener**를 사용했었고
기본 코드는 몇 줄 되지 않습니다.

**val adapter = NoticeAdapter(items.toMutableList(), viewModel, listener)**

함수 파라미터값으로 **NoticeItem**이라는 **data class** 껍데기를 받고서 **adapter**를 정의합니다.

**binding.noticeRv.layoutManager = GridLayoutManager(context, 1)**

처음 설명드렸던 **LayoutManager**가 여기서 등장합니다. 
일반 **LayoutManager**를 사용해서 **vertical**로 아이템을 배열해도 되고 
**GridLayoutManager**를 사용해서 격자 배열로 설정할 수도 있습니다.

**binding.noticeRv.adapter = adapter** 

이제 **Layout** 형태를 정하고 **Adapter**에 넣을 아이템까지 지정했다면 **view binding**을 통해 실제 **RecyclerView**와 연결합니다.

## Fragment 중략 코드

```kotlin
class NoticeFragment : Fragment(), NoticeAdapterListener {

    private var _binding: FragmentNoticeBinding? = null

    private val binding: FragmentNoticeBinding
        get() = requireNotNull(_binding){"FragmentNoticeBinding -> null"}

    private lateinit var listener: NoticeAdapterListener
    private lateinit var noticeAdapter: NoticeAdapter
    
    // 중략...

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        _binding = FragmentNoticeBinding.inflate(inflater, container, false)

        listener = object : NoticeAdapterListener {

            override fun onDeleteNotice(alarmId: Int, position: Int) {}

            override fun onFriendRequestApprove(name: String) {}

            override fun onFriendRequestItemClick(item: NoticeItem.NoticeFriendRequestItem) {}

            override fun onFriendRequestAcceptedItemClick(item: NoticeItem.NoticeFriendRequestAcceptedItem) {}

            override fun onFriendCardItemClick(item: NoticeItem.NoticeCardCheckItem) {}
        }

        return binding.root
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        navController = Navigation.findNavController(view)
        
        // 중략...
    }

    private fun setupRecyclerView(items: List<NoticeItem>) {
        val adapter = NoticeAdapter(items.toMutableList(), viewModel, listener)
        binding.noticeRv.layoutManager = GridLayoutManager(context, 1)
        binding.noticeRv.adapter = adapter

        val swipeToDeleteNotice = SwipeToDeleteNotice().apply {
            setClamp(resources.displayMetrics.widthPixels.toFloat() / 5)
        }
        ItemTouchHelper(swipeToDeleteNotice).attachToRecyclerView(binding.noticeRv)

        binding.noticeRv.apply {
            setOnTouchListener { v, _ ->
                swipeToDeleteNotice.removePreviousClamp(this)
                v.performClick()
                invalidateItemDecorations()
                false
            }

            setOnClickListener {
            }
        }
    }

    override fun onShowDialog() {
        noticeDialogViewModel.setDialogData(
            title = "존재하지 않는 \n 사용자입니다",
            leftButtonText = "확인",
            leftButtonClickAction = { checkUserNone() },
        )
        noticeDialog = NoticeDialog()
        noticeDialog?.show(parentFragmentManager, "CustomDialog")
    }

    override fun onFriendRequestApprove(name: String) {
        val myName = userViewModel.nickname.value ?: ""
        socialViewModel.patchApprove(name, myName)
    }

    override fun onDeleteNotice(alarmId: Int, position: Int) {
        viewModel.deleteNotice(alarmId, position)
        noticeAdapter.removeItem(position)

        // RecyclerView 간격 재설정
        binding.noticeRv.post {
            binding.noticeRv.invalidateItemDecorations()
        }
    }

    override fun onFriendRequestItemClick(item: NoticeItem.NoticeFriendRequestItem) {
        navController.navigate(R.id.action_navigation_notice_to_social_fragment)
    }

    override fun onFriendRequestAcceptedItemClick(item: NoticeItem.NoticeFriendRequestAcceptedItem) {
        navController.navigate(R.id.action_navigation_notice_to_social_fragment)
    }

    override fun onFriendCardItemClick(item: NoticeItem.NoticeCardCheckItem) {
        navController.navigate(R.id.action_navigation_notice_to_home_fragment)
    }

    override fun onDestroyView() {
        super.onDestroyView()
    }
}
```

## 🔥 미션

---

## ✅ 6주차 미션 체크리스트

---

<aside>
💡 미션은 아래 내용을 확인해주세요!

- [ ]  item_album 레이아웃 만들기
    - 아이템의 레이아웃 크기는 `wrap_content`로 지정해 주셔야 합니다.
    
    ![Untitled](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/Untitled.png)
    
- [ ]  리사이클러뷰를 사용해서 화면 만들기
    - 보관함 화면 만들기
    (실제 Flo에서는 이용권을 구입하지 않으면 저장한 곡에 노래가 들어가지 않아서, 비어있을 겁니다. 그거는 신경쓰지 말고, 아래 첨부한 화면대로 만들어오시면 됩니다.)
    - RecyclerView 적용(노래 리스트)
    ⇒ 더미데이터로 아무거나 집어넣어도 됩니다. 다만 최대한 중복되지 않은 데이터로 넣어주세요.
        
        ![Untitled](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/Untitled%201.png)
        
    
- [ ]  리사이클러뷰 클릭 이벤트
    - [보관함] 아이템의 [...] 버튼 클릭시 아이템 삭제
    - [오늘 발매 음악] Play 버튼 클릭 시 MiniPlayer에 동기화
        - 전체 수록곡 중에 가장 처음 곡이 재생되도록 (노래중 하나만 재생되도록 해보기)
    
    ![Untitled](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/Untitled%202.png)
    
- [ ]  [보관함] Item에 스위치를 넣고 item 개수를 늘린 다음 스위치를 ON 한 다음 스크롤했을 때 스위치 ON/OFF가 이상하게 설정되는 문제 해결해보기
    - 하나의 스위치만 ON하고 스크롤을 했을 때 ON하지 않은 곳에 체크되는 현상 or 돌아왔을 때 체크가 되어있지 않는 현상을 해결하기
- [ ]  Foreground Service를 사용하여 알림창 띄우기 **[선택]**
    
    (참고자료의 가장 마지막 부분의 자료를 확인해 주세요. 해당 미션은 Flo 앱의 메인 화면에서 진행해도 괜찮고 새로 프로젝트를 생성한 뒤 구현해도 괜찮아요!)
    
    - 알림창의 아이콘, 타이틀, 내용을 변경해 보고 앱을 내린 뒤 알림 창 클릭 시 해당 앱이 띄워지도록 설정하기
    - Thread 또는 Coroutine을 활용하여 1 ~ 1000까지 숫자를 카운트하고 알림창에 진행 상황을 progress bar로 나타내기 (가능하다면 Coroutine을 사용해 보세요.)
        - 앱을 내려도 Background에서 카운트가 증가하고 progress bar가 작동하도록 설정하기
</aside>

## ❤️‍🔥 6주차 시니어 미션

---

<aside>
💡 실전미션을 통해 Demoday를 대비해보자!

- [ ]  시중에 출시된 앱 내 RecyclerView 페이지 구현하기
    - [ ]  더미 데이터들로 구성된 RecyclerView가 스크롤이 잘되는지 확인해보기
    
    ![image.gif](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/image.gif)
    

![preview.gif](Chapter%206%20RecyclerView%20&%20Adapter%201e9b57f4596b80ec8087f2cfa50c474a/preview.gif)

- 선택한 앱의 **BottomNavigationView**는 2주차에서 실습했던 코드를 복제해서 구현해놓고 RecyclerView로 구현할 부분인 목록 페이지를 **Activity**가 아닌 **Fragment**로 제작하시면 됩니다! 
왜냐하면 **bottomNavigationView Activity** 위에서 화면 전환시 등장하는 화면들은 모두 **Fragment**로 이루어져있기 때문입니다.
- 수많은 데이터들을 목록으로 표시하기 위해서 **RecyclerView**는 필수적인 요소입니다. 
Udemy FLO 앱 클론 코딩에서는 곡 리스트들을 구현하시고 나서 이번 실전미션에서는 여러분들이 평소에 사용하는 앱들 중에서 하나를 선택해서 **RecyclerView** 페이지 부분만 직접 구현해보시면 됩니다. 
강의를 통해서 진행했던 **RecyclerView**와 유사한 구조를 가지면 실습에 전혀 의미가 없기 때문에 시중의 앱을 선택하셔서 최대한 똑같이 구현해보세요.
- 새로고침 효과를 포함한 각종 로딩 효과에 대한 실습은 부록 부분에서 진행할 예정이지만 여유가 된다면 구현해보시는 것도 괜찮습니다.
- ⚠️ 주의사항: 새 프로젝트를 생성해서 제작
</aside>

## 📋 6주차 개발일지

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
💡 스스로 해결하기 어렵다면? 스터디원들에게 도움을 요청하거나 **너디너리의 지식IN 채널에 질문**해보세요!

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

https://www.youtube.com/watch?v=aa6e7GNRyJo&feature=youtu.be

https://www.youtube.com/watch?v=ao0Iqfhy0oo

https://www.youtube.com/watch?v=jsjYo-xy3EA

https://www.youtube.com/watch?v=IaIuKbEyGnY

https://www.youtube.com/watch?v=d9noN4mVHSc

---

Copyright © 2025 Daemon(정승원) All rights reserved.