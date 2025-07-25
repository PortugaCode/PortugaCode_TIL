## CocoaPods (Unity IOS 관련)

<br>

## 

>  🍎 CocoaPods란?

- iOS와 macOS 앱에서 외부 라이브러리를 쉽게 관리하고 설치할 수 있도록 도와주는 **“의존성 관리 도구”**

<br>

마치 Unity에서 `Package Manager`로 `TextMeshPro`나 `Addressables` 같은 걸 설치하는 것처럼,  
iOS에서는 `CocoaPods`를 사용해서 `Firebase`, `Kakao SDK`, `GoogleSignIn`, `Alamofire` 등 수많은 외부 라이브러리를 쉽게 가져다 쓸 수 있다.

<br>

> ## **🔧 CocoaPods가 왜 필요한가?**

<br>

1. **라이브러리 설치 자동화**
    - 예전엔 라이브러리 .framework, .a, .h 파일들을 수동으로 복사하고, Build Setting도 직접 설정해야 했다.
    - CocoaPods는 한 줄 명령어 (pod install)로 이 모든 걸 자동으로 해준다.

<br>

* * *

<br>

2. **버전 관리 용이**
    - PodFile에 설치하고 싶은 라이브러리와 버전을 명시하면, 매번 동일한 환경을 누구나 재현할 수 있다. (협업, 배포 시 매우 중요)

<br>

```
pod 'Firebase/Auth', '10.3.0'
```

<br>

* * *

<br>

3. **의존성 트리 자동 해결**
    - 예: Firebase를 쓰면 내부적으로 여러 모듈(FirebaseCore, FirebaseInstallations 등)이 필요함.
    - CocoaPods가 이걸 알아서 찾아서 설치한다.

<br>

* * *

<br>

4. **통합된 빌드 환경 제공**
    - **pod install** 후 생성되는 **.xcworkspace** 파일을 열면, Xcode 프로젝트와 외부 라이브러리가 하나의 워크스페이스에서 통합되어 빌드됨.
    - 수동 링크 없이도 안정적으로 작동

<br>

* * *

<br>

5. **커뮤니티 및 생태계 기반**
    - iOS 오픈 소스 라이브러리의 대부분이 CocoaPods를 통해 배포됨.
    - 예: Kakao SDK도 `pod 'KakaoSDK'`, Firebase도 `pod 'Firebase/Core'`

<br>

> ##  **📦 CocoaPods 작동 방식 간단 요약**

<br>

- `pod init`: **Podfile이 없을 때** 사용하는 명령어 (초기 설정용)
- `pod install`: **Podfile이 이미 존재할 때** 실행하여 라이브러리를 설치함

<br>

1. `Podfile` 파일 생성: 내가 사용할 라이브러리를 선언.
2. `pod install`: 선언한 라이브러리를 다운로드 + 설치.
3. `.xcworkspace` 생성: Xcode 프로젝트 + Pods 통합된 워크스페이스.
4. `.xcworkspace` 열기: 실제 앱 실행은 이 파일 기준으로 이뤄져야 함.

<br>

```
cd MyUnityIOSProject/
pod init             # → Podfile 생성 (빈 상태)
vim Podfile          # → 원하는 SDK 추가 (예: pod 'Firebase/Auth')
pod install          # → SDK 실제 설치 및 .xcworkspace 생성
open MyProject.xcworkspace
```

## <br>

### 1️⃣ `pod init` 실행 전

```
bash
복사편집
$ ls
Unity-iPhone.xcodeproj
```

### 2️⃣ `pod init` 실행 후

```
bash
복사편집
$ ls
Unity-iPhone.xcodeproj
Podfile         👈 생성됨
```

### 3️⃣ `Podfile` 내용 추가 후

```
ruby
복사편집
target 'Unity-iPhone' do
  pod 'Firebase/Auth'
end
```

### 4️⃣ `pod install` 실행 후

```
bash
복사편집
$ ls
Unity-iPhone.xcodeproj
Podfile
Podfile.lock
Pods/                      👈 설치된 라이브러리
Unity-iPhone.xcworkspace   👈 이걸로 Xcode 열어야 함
```

  

- Unity의 `Packages/manifest.json` → iOS의 `Podfile`
- Unity Package Manager가 패키지 설치 → CocoaPods의 `pod install`
- Unity는 패키지 설치 후 에디터에 반영됨 → CocoaPods는 `.xcworkspace` 생성으로 반영됨
- <br>

## ✅ 언제 반드시 써야 하나?

- Firebase, Kakao, GoogleSignIn 등 네이티브 SDK를 연동할 때
- Unity + iOS 네이티브 기능을 같이 써야 할 때 (예: 푸시알림, SNS 로그인 등)

* * *

## 🚫 안 써도 되는 경우?

- 오직 Unity만으로 구현하고, iOS Native SDK와의 연동이 필요 없는 경우
- 별도 외부 프레임워크가 필요 없는 최소 iOS 빌드일 경우