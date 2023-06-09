# lesson14. 스위치의 구조

## 1. MAC 주소 테이블이란?

- 스위치는 데이터 링크 계층에서 동작하고, Layer 2 Switch 또는 스위칭 허브라고 불린다. 허브와 스위치는 생김새는 구분하기 힘들지만, 하는 역할은 완전히 다르다.

  ![Untitled](https://user-images.githubusercontent.com/63203480/236380243-3dbdf2b1-d37a-4b7b-bb7f-094722cc7cd0.jpeg)

- 스위치 내부에는 MAC 주소 테이블이라는 것이 있다. MAC 주소 테이블(or 브릿지 테이블)은 **스위치의 포트번호**와 **해당 컴퓨터와 연결되어 있는 컴퓨터의 MAC 주소가 등록**되어 있는 데이터베이스이다.
- 목적지 MAC 주소가 포함되어 있는 프레임이라는 데이터가 전송되면 MAC 주소 테이블을 확인하고, 만약 MAC 주소가 등록되어 있지 않다면 MAC 주소를 포트와 함께 등록한다. 이것을 MAC 주소 학습 기능이라고 한다. 이것은 허브(더미 허브)에는 없는 기능이다.
- **수신 측 MAC 주소가 MAC 주소 테이블에 등록되어 있지 않아서 송신 컴퓨터 이외의 컴퓨터들에게 데이터(프레임)가 전송**되는데 이것을 **플러딩**이라고 한다.

  ![Untitled2](https://user-images.githubusercontent.com/63203480/236380288-f21daadf-ebb9-4f39-b67c-32d202740ec0.png)

  만약 MAC 주소 테이블에 MAC 주소가 등록되어 있다면 MAC 주소에 해당하는 포트를 알고 있기 때문에 다른 컴퓨터에게는 데이터가 전송되지 않고, 목적지 MAC 주소에게만 데이터가 전송된다. 그리고 **MAC 주소를 기준으로 목적지를 정하는 것을 MAC 주소 필터링**이라고 한다.

  ![Untitled3](https://user-images.githubusercontent.com/63203480/236380328-bc80aae9-4131-4de8-8499-4928f82fc01b.jpeg)
