# TIL

### 백엔드 아키텍처

---

#### 1. 논의 사항
- 모듈간 동기성 연결로써 gRPC(Google Remote Procedure Call) 채택하는 것이 효율적인가?
  - 프로젝트는 완전한 모놀리식으로 구성할 것이라면 오버엔지니어링이므로 불필요
  - 즉 하나의 서버 내에서 작동하므로 모듈 간 함수 호출이면 충분함
  - 그러나 MSA 구조를 일부라도 채택할 경우 gRPC를 적용하는 것이 좋음. 각 모듈을 독립 서비스로 컨테이너화하기에 유리하기 때문.
  
- LLM → FDS 사이 비동기 처리는 Redis Pub/Sub 구조를 채택하는 것이 효율적인가?
  - Redis Pub/Sub 구조를 채택해도 좋을 것 같음. 아키텍처에 크게 구애 받지 않고 후처리, 병렬 처리, 결합도 분리에 유리하기 때문.
   
- MCP를 사용하는 것이 효율적인가?
  - MCP는 오버엔지니어링이므로 불필요
  - 프로젝트의 입력 채널이 음성 앱 하나뿐이므로 MCP의 강점인 ‘멀티 채널인 경우 동일한 시스템으로 데이터 처리’한다는 강점을 이용할 수 없기 때문입니다.
  - 또한 백엔드 아키텍처를 모놀리식으로 채택할 것이라면 입력 구조가 간단하므로 MCP를 적용할 필요 없음
  - 그리고 이미 클라이언트에서 NLU/DM 처리를 하고 있으므로 MCP를 적용할 경우 구조가 중복되어 비효율적일 가능성이 있음.

 ---

#### 2. 폴더 구조 및 아키텍처
- 
