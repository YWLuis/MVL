# MVL QA 과제 Report
## 작성자: 전영우, youngwoochon@naver.com
## 핵심 Feature
- GPS를 기반한 Rider와 Driver의 정확한 위치 공유
- 위치 공유를 통한 Rider와 Driver의 연동
- Rider의 목적지에 최적화된 거리와 정확한 금액 산정
- QR Code와 Credit card의 연동 결제 
- 7일 전 차량을 예약할 수 있는 Schedule
## 테스트 목적 
QA 과제 진행을 위한 TADA 앱 내 상품 검색 후, Call 수행까지의 과정을 테스트 케이스로 작성하기 위함. 

다른 Feature가 업데이트되더라도 daily로 수행해야 할 필수 검증 시나리오도 포함하였음. 
## 테스트 범위
- 홈화면의 [BOOK CAR/TAXI] 내 진입하여 Drvier Call Request
## 테스트 앱 버전 
- iOS Testflight, 4.7.7 (736.0) 
## 테스트 기기 
- iPhone 12 Pro, iOS 16.1.1
## 테스트 설계서 (Mind Map) 

<img src="https://user-images.githubusercontent.com/119469200/205450282-6271d72f-f457-4e10-a8d9-2416700680e7.png" width="400" height="200" />

## Daily 필수 검증 시나리오 
- [호출] 사용자가 현재 위치에서 TADA app의 Google Map과 일치 여부
- [호출] 목적지 주소를 입력한대로 Google Map에 정확히 입력 검증 
- [호출] 출발지와 목적지의 거리와 예상 시간, 각 차종의 가격이 합리적인 여부 
- [결제] Cash 이외 QR과 Credit Card를 통한 결제의 정상 동작 검증 
- [결제] Voucher 검증 
- [결제] Schedule의 5가지의 조건의 동작 여부 
- [결제] General Call과 Smart Call의 동작 검증 
- [정산] Rider는 결제, Driver는 정산 검증 

## 테스트 케이스
### Precondition
- 정상 회원 상태의 로그인을 완료한 사용자
- 휴대전화 번호 인증을 완료한 사용자

|TC No.|Category|Precondtion|Steps&Action|Expected Results|Result|P/F|Remarks
|---|---------------------|---|---|---|---|---|---|
|1|Set pickup Location|- 정상 회원 상태의 사용자가 로그인 완료 <br> - 앱의 위치 동의를 허용한 사용자|1. 홈화면에서 [Book Car/Taxi]를 선택|1. App의 위치동의가 허용되었을 경우, Google Map의 사용자의 현재 위치가 표시되어야 한다. <br> 2. App의 위치동의가 허용되지 않았을 경우, 싱가폴 현지 내 Google Map으로 노출되어야 한다. <br> 3. 노출되어야 할 항목들은 아래와 같다 <br> - GPS <br> - Text를 입력할 수 있는 [To] <br> - PIN의 위치를 To로 지정할 수 있는 Set pickup location||| |
|2|Set pickup Location 내 Google Map||1. Google Map 화면에서 슬라이드, 확대, 축소를 수행 <br> 2. 현재 GPS에서 인식한 위치를 선택 후, [Set pickup location]을 선택|1-1. GPS 기반한 장소가 아닐 경우, 위치를 확인하라는 팝업창이 나타나야 한다. <br> 1-2. GPS 기반한 장소의 근처일 경우, PIN의 위치한 address가 나타나야 한다. <br> 2. [Map], [From], [To], [Addtional stop], [Home], [Office], [Favourite], [Airport], Recent locatio 등이 노출되어야 한다.|||
|3|Set pickup Location 내 출발지, 도착지 입력 페이지|- TC No. 2 완료|1. [To]와 [From]의 Address를 입력|1. 2개의 Address가 입력된 동시에 Google Map에 From은 1, To는 2로 표기되며, Address도 표기되어야 한다. <br> 2. 1과 2사이에 거리가 검정색으로 표기, 최적의 거리로 노출되어야 한다. <br> 3. 차량은 기본값 AnyTADA로 나타나야 한다. <br> 4. 금액은 거리 비례 측정된 금액으로 나타나야 한다. <br> 5. 예상 시간이 나타나야 한다. <br> 6. 그 외 Payment, Voucher, Family, Note to Driver, Trip purpose, Set time 등이 노출되어야 한다. <br> 7. [Book]이 나타나야 한다. |||
|4|이동거리 확인 페이지||1. Select Car Type을 선택 <br> 2. 상세페이지 진입 후, 임의의 차종을 선택한다. |1. 11종의 차종이 나타나야 한다. <br> 2. 선택한 차종이 적용되며, 아이콘과 금액이 확인 페이지에 적용되어야 한다. |||
|5|이동거리 확인 페이지||1. Payment를 선택 <br> 2. Cash를 선택 <br> 3. NETS QR을 선택 <br> 4. OBCB Pay Anyone을 선택 <br> 5. [Add Card]를 선택|Expected|||
|6|Payment Method||1. [Add Card]를 선택 <br> 2. 카드사를 선택 |1. [Add Card]를 선택 <br> 2. 카드사를 선택 |||
|7|Vouchers||1. Voucher를 선택 <br> 2. Valid/Invalid의 Promotion Code를 입력 <br> 3. 등록된  Voucher에서 Detail, Use 항목을 선택|1. Voucher 페이지로 전환되어야 한다. <br> 2-1. Valid Voucher일 경우, 할인금액과 함께 등록되어야 한다. <br> 2-2. Invalid일 경우, 등록불가 팝업 메시지가 노출되어야 한다. <br> 3-1. Detail을 선택했을 경우, 해당 쿠폰의 상세 페이지로 전환되어야 한다. <br> 3-2. Use를 선택 시, 확인 페이지로 전환되며, 쿠폰이 적용된 금액으로 적용되며, Voucher란의 사용된 쿠폰명이 나타나야 한다. <br> 3-3. 선택된 쿠폰을 [Use Later] 선택 시, Voucher 적용이 해제되어야 한다. |||
|8|Scheduel|- iONTADA와 Metered 차량은 제외되어야 한다. <br> - Credit Card가 등록된 정상 상태의 사용자|1. Precondition의 차량을 제외한 차량을 선택 <br> 2. [Set Time Call Now]를 선택 <br> 3. Pick Up Date, Pick Up Time을 선택 <br> 4. Schedule을 선택|1. 하단에 [Set Time Call Now]가 나타나야 한다. <br> 2. Set Time 페이지로 전환되며, Booking Fee, Pick Up Date, Pick Up Time, Schedule이 나타나야 한다. <br> 3. 오늘을 포함한 일주일의 다음 날짜들이 나열되어야 하며, 시간은 HH:MM이 선택 가능하여야 한다. ||| - Credit Card를 등록하지 못하여 Step No. 4 이후로 테스트하지 못했음
|9|Call Confirmation||1. [Book]을 선택 <br> 2. General call 또는 Smart call을 선택 후, Request 선택|1. General Call과 Smart Call 선택 항목이 나타나야 한다. <br> 2. Processing 페이지가 노출되어야 하며, From to, Estimated Fare, Car Type, Payment Method 및 [Cancel]이 나타나야한다. <br> 3. Call이 실패될 경우, Smart call 권유 및 Retry 항목이 나타나야 한다. |||
|10|운행완료 후||1.  Driver가 지정한 위치에 도착 <br> 2. Rider가 지정한 방식으로 지불 <br> |1. 도착한 위치가 Driver, Rider, Admin에게 공유 <br> 2. Admin이 확인 후, Rider에게 정산|||

## 탐색적 테스팅
### Issue 1: Google Map에서 싱가폴 지역을 벗어날 경우, 홈화면으로 돌아감 

#### 문제의 내용 

위치 지정 시, Singapore가 아닌 동남아시아를 벗어난 지역을 선택할 경우, App이 홈화면으로 돌아갑니다. 

#### 재현 방법 

1. 홈 -> [BOOK CAR/TAXI]를 선택

2. Google Map에서 최소한으로 축소한 뒤, 고정 핀을 동남아시아 지역이 아닌 곳으로 이동 

3. [Confirm Pick-up Location]이라는 팝업과 함께 홈화면으로 돌아간 것을 확인 

#### 재현된 사진

<img src="https://user-images.githubusercontent.com/119469200/205448838-b7a816f3-0b23-4845-ab4f-af15b1e4c3ef.jpeg" width="200" height= "400" />

#### 재현율 

100% 

#### Expected Result 

1. 싱가폴의 먼 지역을 선택했을 때와 마찬가지로 Google Map은 유지하되, [Confirm Pick-up Location] 문구가 나타나야 합니다. 

### Issue 2: Driver call 응답이 없을 경우, 애플워치 메시지 시간이 고정되어 있음 

#### 문제의 내용 

Drvier call 응답이 없을 경우, 애플워치로 instance message를 보내는데, 해당 메시지의 시간이 고정적으로 2개의 알림이 나타납니다. 

#### 재현 방법

- Precondition - 애플워치와 연동된 아이폰

1. [BOOK CAR/TAXI]에서 Call 단계까지 진행 후, Request를 수행한다. 

2. Request 신호 확인 후, 앱을 백그라운드로 운용(디바이스 홈화면으로 이동)하거나 화면을 잠금화면으로 전환한다 

3. Request 실패 시, 애플워치에 알림이 오는 것을 확인한다. 

#### 재현된 사진

<img src="https://user-images.githubusercontent.com/119469200/205449064-8f6e8593-52a5-49a9-a6a0-58baba965837.png" width="200" height="400" />

#### 재현율 

100% 

#### Expected Result

1. Instance message에 표기되는 시간과 사용자가 보는 시간에 맞춰 표기되어야 합니다. 

### Issue 3: NETS QR, Smart Call 호출 시, 상단 UI가 가려짐 

#### 문제의 내용 

사용자가 결제 수단을 NETS QR, Call 방식을 Smart Call로 Request할 경우, 상단의 NETS QR이 Smart Call의 UI를 가리고 있습니다. 

#### 재현 방법 

1. [BOOK CAR/TAXI]에서 Call 단계까지 진행한다. 

2. Payment method는 NETS QR을 선택한다. 

3. Request 전 call method는 Smart Call을 선택한다. 

4. 두 개의 이미지가 겹쳐지는 것을 확인한다. 

#### 재현된 사진 

<img src="https://user-images.githubusercontent.com/119469200/205449275-b7ec2577-c5bb-4047-9edd-196fc74bb62c.png" width="200" height="400" />

#### 재현율

100% 

#### Expected Result

1. 두 개의 이미지가 겹쳐보이지 않아야 합니다. 


### 확인이 필요한 사항

1. 싱가폴 이북의 말레이시아 지역인 JOHOR, Pasir Gudang까지 Request가 가능한 데, 내부 정책이 궁금합니다. 

2. Favourite Spot에서 Edit Spot 시, 주소를 입력할 수 있는데 글자 제한이 없으며, 입력 후, 바로 Recent Favorite에 적용되지 않습니다. 

3. Payment에서 카메라 허용을 거부하면 App 내에서 다시 허용으로 변경할 수가 없습니다. 

4. Payment의 Add Credit Card에서 Union Pay로 카드 등록 후, OTP 입력 시 무한로딩이 되는 현상이 있습니다. 

5. Request 실패 시, [Smart call], [Retry]가 나타나는 데, General call, Smart Call 모두 동일하게 나타나지만, Smart Call일 경우, 두 개의 차이가 없는 것 같습니다. 
