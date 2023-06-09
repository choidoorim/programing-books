# lesson20. 네트워크 주소와 브로드캐스트 주소의 구조

## 1. 네트워크 주소와 브로드캐스트 주소란?

- 생성 가능한 IP 주소는 네트워크 주소와 브로드캐스트 주소를 제외한 `2^(호스트ID Bit) - 2` 개이다.
- IP 주소는 네트워크 주소와 브로드캐스트 주소가 있는데, 이 두 종류의 주소는 특별한 주소로 절대로 컴퓨터나 라우터가 자신의 주소로 사용할 수 없다.
- 네트워크 주소는 호스트 ID 가 10진수로 0이고, 2진수로는 `00000000` 인 주소이다. 브로드캐스트 주소는 호스트 ID 가 10진수로 255이고, 2진수로는 `11111111` 인 주소이다.

    ```
    																												{호스트주소}
    네트워크 주소:    192.168.1.0 → 11000000.10101000.00000001.00000000 
    브로드캐스트 주소: 192.168.1.255 → 11000000.10101000.00000001.11111111 
    ```


### 네트워크 주소

- 네트워크 주소는 전체 네트워크에서 작은 네트워크를 식별하는데 사용한다.
- 호스트 ID 가 0 일 경우, 그 **네트워크 전체를 대표하는 주소**가 된다. 예를 들면 `192.168.1.1 ~ 192.168.1.6` 까지의 IP 주소를 가진 컴퓨터는 `192.168.1.0` 이라는 네트워크 안에 속해져 있는 것이다.

### 브로드캐스트 주소

- 네트워크에 있는 컴퓨터나 장비 모두에게 한 번에 데이터를 전송하기 위해 사용되는 전용 IP 주소이다. 만약 전체 네트워크에 데이터를 전송하려면 호스트를 255 로 설정(`192.168.1.255`)하면 된다. 예를 들어 `192.168.1.255` 라는 주소에 데이터를 전송한다면 네트워크 안에 있는 `192.168.1.1 ~ 192.168.1.6` IP 주소를 가진 컴퓨터에서 모두 데이터를 받는다. 그렇기 때문에 네트워크 주소와 브로드캐스트 주소는 절대 자신의 IP 주소로 설정하면 안된다.
