- 허브: 패킷을 중계하는 장치
  - 리피터 허브
  - 스위칭 허브
- 라우터: 패킷을 중계하는 장치
- 서브넷: 허브에 몇 대의 PC가 접속된 것
- IP 주소: 네트워크 번호 + 호스트 번호
  - 호스트번호 → 서브넷 내에서 장치를 구별하기 위해 사용
  - 192.168.12.1
- 넷 마스크(서브넷 마스크): 네트워크 번호와 호스트 번호를 구분하기 위해 사용
  - 192.168.12.1/255.255.255.0
  - 255 부분이 네트워크 번호 0 부분이 호스트 번호
  - 호스트 번호가 0인경우 서브넷 자체를 나태내고 255인 경우 브로드캐스트를 나타냄
- DNS 리졸버: 사용자가 도메인을 이름을 입력하면 해당 도메인에 대한 IP주소를 찾아 반환해주는 역할
  - 소켓 라이브러리에 들어있는 부품화한 프로그램
- DNS 리졸루션 → DNS 리졸버가 IP 주소를 찾는 과정
  1. 도메인 이름 확인
  2. 로컬 캐시에 저장된 정보 확인
  3. 정보가 없는 경우 가까운 DNS서버부터 시작해 재귀적으로 도메인 이름에 대한 IP주소 요청
     - **루트 DNS 서버**:
       - 사용자의 DNS 리졸버가 루트 DNS 서버에 쿼리를 보냅니다.
       - 루트 DNS 서버는 `.com` TLD DNS 서버의 주소를 반환합니다.
     - **TLD DNS 서버**:
       - DNS 리졸버가 `.com` TLD DNS 서버에 쿼리를 보냅니다.
       - TLD DNS 서버는 `example.com` 도메인의 권한 있는 DNS 서버의 주소를 반환합니다.
     - **권한 있는 DNS 서버**:
       - DNS 리졸버가 `example.com`의 권한 있는 DNS 서버에 쿼리를 보냅니다.
       - 권한 있는 DNS 서버는 `www.example.com`의 IP 주소를 반환합니다.
  4. IP 주소를 얻으면 사용자에게 제공하고 캐시에 저장
- 메시지 송신 동작은 리졸버가 하는것이 아닌 OS내부의 프로토콜 스택을 통해 실행

### 궁금해

- 8.8.8.8 구글 DNS 서버 혹은 1.1.1.1 cloudflare DNS 서버는 루트, TLD, 권한있는 DNS 서버중 어디에 속하는 걸까?
  - 모두 해당하지 않음 → 재귀 DNS 리졸버로 사용자의 요청을 받아 여러 DNS 서버들과 통신해 IP주소를 알아내는 역할
