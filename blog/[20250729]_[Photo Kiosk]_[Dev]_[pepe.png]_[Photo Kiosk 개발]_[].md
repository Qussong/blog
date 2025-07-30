# Photo Kiosk

### 📌화면 구성안
#### 하나의 Canvas + 여러 Panel 
화면 전환이 자주 일어나고, UI 요소 간 공유가 많을 때 추천된다.</br>
✅장점 :</br>
    - 씬 전환 없이 빠른 UI 전환 가능</br>
    - UIManager로 Panel 활성/비활성만 조절하면 됨</br>
    - 애니메이션 전환이나 페이드 효과 구현이 쉬움</br>
    - 메모리 관리가 효율적 (씬 로딩이 없음)</br>

⚠️단점 :</br>
    - 모든 UI가 한 씬에 있어 Hierarchy가 복잡해질 수 있다.</br>
    - 초기 로딩 시 모든 UI 리소스를 불러올 수 있다.</br>
#### 각 화면을 별도의 Canvas로 구성
추천 상황 : 각 화면이 독립적이고, UI 요소가 복잡하거나 무거울 때 추천된다.</br>
✅장점 :</br>
    - UI 분리가 명확해 유지보수에 유리</br>
    - 각 Canvas에 독립적인 카메라/레이어 설정 가능</br>
    - Scene 분리도 고려 가능 (ex. 메인화면은 별도 Scene)</br>

⚠️단점 :</br>
    - 화면 전환 시 Canvas 간 활/비활성 관리 필요</br>
    - 전환 애니메이션 구현이 복잡할 수 있다.</br>

#### 실무 팁 by GPT
대부분의 모바일 앱이나 게임에서는 하나의 Canvas에 여러 Panel을 두고 SetActive() 로 전환하는 방식이 일반적이다.</br>
SceneManager 또는 UIManager 클래스를 만들어 Panel 전환을 관리하면 깔끔하게 유지할 수 있다.</br>

#### 화면 구성
- 메인화면 (Main) : Intro</br>
- 촬영화면 (Camera) : 촬영</br>
- 편집화면 (Edit) : 사진 선택 및 보정</br>
- 결과화면 (Result) : 결과 확인</br>
- 인화화면 (Print) : 사진 출력 대기 및 QR 코드</br>

### 📌포토키오스크 프레임 종류
#### 참고
인생네컷, 포토큐, 셀피스탠드
#### 프레임 종류
- 인생네컷 : 4/6/8컷 프레임, 스토리 에디션, 멀티프레임, 콜라보프레임, 나만의 프레임</br>
- 포토큐 : 베이직/컬러/캐릭터/시즌/이벤트/커플/우정/흑백/빈티지 프레임</br>
- 샐피스탠드 : 1/3/4컷 프레임, 기본형 프레임 7종, 커스터마이징 프레임, 이벤트용 프레임, 캐릭터 프레임</br>

### 📌클래스

#### 클래스 구성 & 네이밍
- Manager Class : 사용자의 입력처리, 흐름제어</br>
    ```plainText
    SceneManager
    PhotoManager
    PrintManager
    ```
- Controller Class : 사용자가 어떤 행동을 했을 때 반응</br>
    ```plainText
    CameraController
    EditController
    UIController
    ```
- Model Class
    ```plainText
    PhotoData
    PrintData
    ```
#### 멤버 할당 방식
|항목|자식 객체 찾기 (transform.Find())|SerializeField 로 Inspector에서 지정|
|:---:|:---|:---|
|장점|코드만으로 자동 연결 가능</br>프리팹 복제에 용이|연결 명확하게 보임</br>컴파일 전에 오류 확인 가능|
|단점|문자열 기반이라 오타 시 런타임 오류발생</br>구조 바뀌면 깨질 위험 존재함|Inspector 연결 누락 시 오류 발생</br>스크립트마다 일일이 설정 필요함|
|추천상황|재사용성이 중요한 프리팹</br>자동화가 중요한 경우|UI 구조 변경이 잦은 프로젝트</br>다른 개발자와 협업 시 직관적|

**명확하고 유지보수가 중요하며, 특히 협업중**이라면 SerizlizeField 로 Inspector에 직접 연결하는 방식이 훨씬 안전하고 효율적이다.</br>

