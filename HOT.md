### 오케스트레이션이란?
가상 자원들의 구성과 설정을 정해진 방식과 순서에 맞게 자동화하는 로직을 통해 
복잡한 인프라의 생성 및 관리를 단순화하고 효율적으로 운영하도록 하는 기술이다.

초기의 실험적 프로젝트에서 Heat는 아마존 웹서비스 (AWS: Amazon Web Service)의 오케스트레이션 서비스인 
클라우드포메이션(CFN: CloudFormation)[5]을 벤치마킹하여 CFN 템플릿을 기반으로 하는 오케스트레이션 엔진을 개발하였다. 
하지만, 공식적인 프로젝트로 진행되면서 HOT(Heat Orchestration Template)라는 자체 템플릿을 정의하였고 
점진적으로 클라우드포메이션의색깔을 벗고 독자적인 오케스트레이션 서비스를 제공하는 방식으로 발전해 가고 있다

### Heat의 구조 
Heat는 여타의 오픈스택 프로젝트와 마찬가지로 Python 언어로 구현되어 있으며 CLI(Command LineInterface) 및 API(Application Programming Interface)서버와 같은 
사용자 인터페이스와 템플릿을 기반으로 가상 자원들을 구성하고 설정하는 로직인 Heat Engine 으로 구성된다.
eat의 기본 구조를 도시한다. 사용자는 API를 직접 호출하여 오케스트레이션 서비스를 요청하거나 CLI를 통해 동일한 작업을 수행할 있다. 
CLI 역시 사용자 명령을 API로 변환하여 처리하게 된다. 
현재 Heat API 서버에서 지원하는 API의 종류는 두 가지로 하나는 아마존 웹서비스의 클라우드포메이션이션 API이고, 또 하나는 Heat에서 독자적으로 정의한API이다. 
두 가지 API 모두 HTTP 프로토콜을 활용하 지만 클라우드포메이션 API는 Query API 방식이며 Heat API는 Restful API 방식을 따른다.

 Heat Orchestartion Template
Heat는 템플릿 기반의 오케스트레이션 서비스를 제공하는 프로젝트로 사용자가 구성하고자 할 가상 자원들을 템플릿에 명시하도록 한다. 템플릿은 JSON(Java-Script Object Notation)이나 YAML(YAML Ain't Mark-up Language)과 같이 사람이 쉽게 읽고 작성할 수 있는 텍스트 기반의 데이터 인코딩 방식을 이용한다. 아마존 웹서비스의 CFN 템플릿이 JSON 기반의 표현 방식을 사용하는 반면 HOT 템플릿은 YAML을 인코딩 방식으로 사용한다. YAML 방식이 JSON 방식에 비해 파싱(parsing)의 부하가 좀 더 크지만 JSON과 달리 멀티라인 스트링을 지원하고 주석 처리가 용이하다는 장점을 갖는다. 
