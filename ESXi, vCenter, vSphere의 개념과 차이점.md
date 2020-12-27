### ESXi, vCenter, vSphere의 개념과 차이점(VMware의 엔터프라이즈 버전에서 가장 많이 사용되고 있는 제품들)

* ESXi란?

  ESXi는 VMware에서 나온 하이퍼바이저(Hypervisor). 하이퍼바이저란 쉽게 이야기하면 가상화 환경을 만들 수 있도록 최소한의 기능만을 지원하는 축소버전의 OS (윈도우즈나 리눅스 같은)라고 이해하면된다. (가상화 환경을 만드는데 소프트웨어의 도움없이 하드웨어를 그냥 사용할 수 없으니까) Configuration과 시스템을 Manage할 수 있는 약간의 기능을 제외하고는 다른 기능들을 지원하고 있지 않다. (예를 들어서 GUI라던가…) 하이퍼바이저는 두 종류가 있는데 (Type 1과 Type 2) ESXi는 Type 1 하이퍼바이저이다.다른 회사에서 나온 경쟁 제품으로 Microsoft에서 나온 Hyper-V와 Citrix에서 나온 XenServer가 있다.

* vCenter란?

  가상화 환경을 만드는 가장 큰 이유는 여러 컴퓨터를 하나의 큰 성능/용량의 컴퓨터처럼 사용하기 위함인데 그 기능을 지원하는 것이 vCenter이다. 다시 말해서 vCenter는 가상화 환경 구축을 위한 핵심 소프트웨어로 ESXi가 설치된 다수의 머신을 하나의 가상화 환경으로 만들어주는 기능을 제공한다. 가상화 시스템 운영자의 입장에서 vCenter를 이용하면 여러 ESXi 호스트들을 쉽게 추가/제거할 수 있으며 그 외에도 아래와 같은 엔터프라이즈 기능들을 제공한다. vMotion: 현재 사용 중인 VM (Virtual Machine)을 VM의 전원을 끄지 않은 상태에서 다른 호스트로 (서버) 이동할 수 있게 해주는 기능DRS (Distributed Resource Scheduler) & DPM (Distributed Power Management): VM의 컴퓨터 리소스 사용 (CPU나 메모리)을 계속 체크하고 경우에 따라 VM을 다른 호스트로 이동하거나 VM의 할당이 되지 않아서 아무런 일을 하지 않는 호스트의 경우 전원을 잠시 꺼두고 필요 시 다시 전원을 키는 등의 리소스 관리를 도와주는 기능이다.

* vSphere란?

  vSphere란 위에 언급한 소프트웨어들을 전부 포함하고 있는 소프트웨어 Suite 또는 패키지를 일컬으며 위의 소프트웨어 외에도 다른 많은 소프트웨어를 포함하고 있다. (예를 들어 vSphere Client 또는 vSphere SDKs) 마이크로소프트 제품인 Office랑 비교하면 vSphere는 Office와 같은 개념이고 ESXi나 vCenter는 Word나 Excel이라고 이해하면 된다. 

  >  설치 및 라이센스에 대한 간략한 정보대부분의 VMware 제품은 VMware 웹사이트(https://my.vmware.com/web/vmware/downloads)에서 무료로 다운로드 받아서 설치할 수 있다. ESXi 같은 경우에는 무료 버전도 있기 때문에 무료로 다운 받아서 사용 가능하다. 그렇지만 vCenter 라이센스는 유료이며 가격도 비싼 편이다. (상당 부분의 VMware 영업이익이 vCenter 라이센스에서 발생된다고 들었습니다.) 사실 ESXi는 단순한 하이퍼바이저이기 때문에 무료로 배포를 한다고 해도 vCenter가 없으면 가상화 환경을 만들 수 없기 때문에 이런 사업 모델을 사용하는게 어떻게 보면 당연하다고 생각하며 이런 점 때문에 OpenStack 같은 오픈 소스 클라우드 플랫폼에 상당히 많은 사람들이 관심을 갖는게 아닌가 생각된다. (OpenStack은 vCenter를 대체할 수 있는 오픈소스 프로젝트로 만약 OpenStack을 사용할 경우 vCenter 라이센스 없이 ESXi 호스트를 이용해서 가상화 환경 구축이 가능하다.)  