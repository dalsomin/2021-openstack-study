Oepnstack Ocata 릴리즈 부터 기본적으로 fernet token 을 기본 토큰 프로바이더로 사용 되고 있다.
기존에 사용 하고 있던 UUID는 스토리지 공간 문제와 네트워크 트래픽 문제가 있으며, 
UUID를 대체하고자 나온 PKI/PKIZ는 큰 공유 캐시 문제와 UUID 보다 느린 성능으로 Ocata 릴리즈에서 아예 제거 되었다.

fernet은 대칭키 암호 인증 방식으로 , 암호화와 복호화에 동일한 키를 사용 한다. Openstack kilo 릴리즈에서 도입 되어 Ocata 릴리즈 부터 기본 token provider 로 지정 되었다.
또한, 다중키를 사용 하여 첫번째(현재키: Primary key)를 사용 하고 다른키(이전키: Secondary Key 및 준비키:Staged Key)를 이용 하여 복호화를 진행 한다. 
이를 통하여 키를 정기적으로 rotation 하여 보안을 강화 하고, 이전키로 만든 토큰은 계속 복호화에 사용 된다.

