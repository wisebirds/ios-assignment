## iOS 과제

### 제출 조건

1. 과제 repo clone 후 개인 github 에 private repository 생성 후 Settings > Collaborators and teams > Manage access > Add People > dy128.kim@wisebirds.com, jinyeong.lee@wisebirds.com 계정을 추가해주세요
2. **제출 방법**: 과제 시작 시간부터 4시간 이내 필수로 push 해주세요.
   (시간이 부족할 경우 6시간 이내 추가로 push 할 수 있지만 추가 검토용으로만 참고될 예정입니다.)
3. **제약 사항**
   - SDK 부분은 UIKit 으로 개발
   - 기타 package 사용 지양 (사용시 사용하게된 이유를 PACKAGE.md 파일에 작성 필요)
   - 그 외에는 제약 사항 없이 자유롭게 구현해주시면 됩니다.
4. **평가 기준**: 기능 구현 완성도 및 설계 품질을 중점 검토 예정입니다.
   - 이미지, 팝업 광고 외에 다양한 형식의 광고가 추가될 수 있다고 가정해주세요.
5. **유의 사항** :
   채용 과제 내용 및 진행 방식에 대한 일체의 정보 및 자료은 회사의 사전 서면 동의 없이 제3자에게 공개, 누설 또는 제공하는 것을 엄격히 금지하고 있습니다.

### 구현 내용

앱에서 흔히 볼 수 있는 이미지 광고와 팝업 광고 개발

#### 1. 광고 SDK 개발

`sdk` 폴더 추가 후 폴더 하위에 다음 모듈들을 구현:

1. **이미지 광고 렌더링 모듈**
   - 이미지 광고를 화면에 표시하는 기능
2. **팝업 광고 모듈**
   - 팝업을 띄워 광고를 렌더링하는 기능
3. **광고 데이터 연동**

   - **광고 위치 마다 query parameter 의 id 값이 다른 API URI 를 사용하게 된다고 생각해주세요.**
   - 광고 데이터는 아래 API 참고
   - API headers

     ```
     {
        apikey: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InppbW9iaHRlamlkYmNzcnVqaHhkIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTgwOTgxNzYsImV4cCI6MjA3MzY3NDE3Nn0.oi_IEKXYWgSUwrCNGVWtZhRf2ys92N028Kp1Km9vOXE",
        Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InppbW9iaHRlamlkYmNzcnVqaHhkIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTgwOTgxNzYsImV4cCI6MjA3MzY3NDE3Nn0.oi_IEKXYWgSUwrCNGVWtZhRf2ys92N028Kp1Km9vOXE"
     }
     ```

     a. 이미지 광고 위치에 필요한 API

     - API URI: https://zimobhtejidbcsrujhxd.supabase.co/rest/v1/ads?select=*&id=eq.1
     - method: GET

     b. 팝업 광고 위치에 필요한 API

     - API URI: https://zimobhtejidbcsrujhxd.supabase.co/rest/v1/ads?select=*&id=eq.2
     - method: GET

4. **노출 추적 기능**
   - 이미지가 화면에 안 보이다가 조금이라도 보일때 `print("on screen")` 호출
   - 이미지가 다시 화면에서 사라진 후 (ex. 스크롤, 팝업 닫기, 앱 전환 등 다양한 경우 있음) 다시 화면에 조금이라도 보이면 `print("on screen")` 호출
   - 이미지가 계속 화면에 보일 경우 반복적으로 호출하지 않음

#### 2. SDK 활용한 광고 구현

개발한 SDK를 사용하여 ContentView에 광고 기능 추가:

1. **이미지 광고**: ContentView 제일 하단에 이미지 광고 배치
2. **팝업 광고**: ContentView 제일 하단에 버튼 추가 후, 클릭 시 팝업 광고 표시
