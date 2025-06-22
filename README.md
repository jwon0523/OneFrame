# 📱 OneFrame - 감정 기반 사진 일기 앱

<br>

## 1. 앱 개요

OneFrame은 사용자의 감정과 하루를 한 장의 사진과 함께 기록하는 감정 기반 사진 일기 앱입니다. 사용자는 하루 동안 느낀 감정을 선택하고, 간단한 텍스트와 사진을 함께 저장할 수 있으며, 주간 단위로 감정 통계를 확인하고 감정 분석 결과를 받아볼 수 있습니다.

<br>

## 2. 주요 기능

### 📝 일기 작성 (Diary Write)
- 사용자는 감정 선택, 제목, 텍스트 작성, 사진 선택 기능을 통해 하루를 기록합니다
- 작성된 일기는 로컬 데이터베이스(Room)에 저장되며, 이미지 파일은 내부 저장소에 저장됩니다

### 📋 일기 목록 보기 (Diary List)
- 작성된 일기를 리스트 형태로 조회할 수 있으며, 일기 상세 페이지로 이동하여 내용을 확인할 수 있습니다

### 🧠 감정 분석 (Emotion Analysis)
- 일주일 동안 작성된 일기를 기반으로 OpenAI API를 호출하여 감정 분석을 수행합니다
- 분석 결과는 원형 도넛 차트와 함께 사용자에게 따뜻한 피드백 메시지로 제공됩니다

### 🏠 홈 화면 요약 (Home)
- 최근 작성된 일기를 썸네일 캐러셀 형태로 보여주며, 주간 감정 요약을 차트로 시각화합니다
- 캘린더에는 일기 작성 여부가 표시되고, 작성된 날짜를 클릭하면 상세 페이지로 이동할 수 있습니다

<br>

## 3. 기술 스택

| 분류 | 기술 |
|------|------|
| **Frontend (UI)** | Jetpack Compose |
| **Database** | Room (SQLite 기반), 싱글톤 구조로 관리 |
| **Image Handling** | 내부 저장소 파일 입출력, Android ContentResolver |
| **AI 감정 분석** | Retrofit + OpenAI API 연동 (ChatGPT) |
| **Navigation** | Jetpack Navigation Compose, 커스텀 라우터 객체 구성 |
| **비동기 처리** | Kotlin Coroutines (suspend, LaunchedEffect) |

<br>

## 4. 구현 구조 및 설계 특징

### 🏗️ View와 Logic 통합 구조
- 학부 수준 프로젝트의 범위와 시간 제약에 따라, 각 화면은 하나의 파일 내에서 UI와 로직을 함께 정의하였습니다
- 단, 추후 MVVM 아키텍처로 분리 가능하도록 로직은 명확히 구조화되어 있습니다

### 🗄️ 싱글톤 DB 접근
- `object DatabaseProvider`를 통해 앱 전체에서 DB 인스턴스를 공유하며, 리소스 낭비를 방지합니다

### 🤖 OpenAI 연동
- Retrofit과 @POST 메서드를 통해 OpenAI Chat Completion API를 호출하고, 사용자 일기 내용을 기반으로 주간 감정 분석과 피드백 메시지를 생성합니다
- 응답 파싱은 Gson을 사용합니다

### 🎨 UI 구성
- `EmotionDonutChartWithLegend`를 통한 원형 차트 시각화
- `LazyRow`/`LazyColumn`을 활용한 리스트/캐러셀 UI
- `Calendar` 컴포넌트를 통한 날짜 기반 UI 제공

<br>

## 5. 핵심 가치

### 💝 정서적 인터페이스
- 단순한 일기 앱이 아닌, AI 감정 분석 피드백이라는 기능을 통해 사용자의 감정을 인식하고 위로하는 정서적 인터페이스를 제공합니다

### ✨ 사용자 친화적 설계
- 일기 작성에 부담을 줄이기 위해 텍스트, 사진, 감정 선택만으로도 하루를 기록할 수 있도록 설계되었습니다

<br>

## 6. 프로젝트 구조

```bash
OneFrame/
├── app/
│   ├── build.gradle.kts
│   ├── proguard-rules.pro
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml
│       │   ├── java/com/example/oneframe/
│       │   │   ├── data/
│       │   │   │   └── DiaryDatabase.kt
│       │   │   ├── navigation/
│       │   │   │   └── NavigationRouter.kt
│       │   │   ├── ui/theme/
│       │   │   │   ├── Color.kt
│       │   │   │   ├── Theme.kt
│       │   │   │   └── Type.kt
│       │   │   ├── utils/
│       │   │   │   └── EmotionUtils.kt
│       │   │   ├── DiaryDetailScreen.kt
│       │   │   ├── DiaryListScreen.kt
│       │   │   ├── DiaryWriteScreen.kt
│       │   │   ├── HomeScreen.kt
│       │   │   ├── MainActivity.kt
│       │   │   ├── MyPageScreen.kt
│       │   │   └── WeeklyEmotionReportScreen.kt
│       │   └── res/
│       │       ├── drawable/
│       │       ├── font/
│       │       ├── mipmap-*/
│       │       ├── values/
│       │       └── xml/
│       ├── androidTest/
│       └── test/
├── build.gradle.kts
├── gradle/
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle.kts
└── README.md
```

<br>

## 7. 개발 환경

- **IDE**: Android Studio
- **Language**: Kotlin
- **Minimum SDK**: API 24 (Android 7.0)
- **Target SDK**: API 34 (Android 14)
- **Build System**: Gradle (Kotlin DSL)
- **Version Control**: Git

## 8. 주요 화면
![image](https://github.com/user-attachments/assets/e2682e99-c5b2-4f65-abc7-046220617030)


### 📱 홈 화면
- 최근 일기 썸네일 캐러셀
- 주간 감정 요약 차트
- 캘린더 뷰

### ✍️ 일기 작성 화면
- 감정 선택 (8가지 감정)
- 제목 및 내용 입력
- 사진 첨부 기능


### 📋 일기 목록 화면
- 작성된 일기 리스트
- 상세 페이지 이동

### 🧠 감정 분석 화면
- 주간 감정 통계(원형 차트)
- AI 피드백 메시지

<br>

## 10. 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다.