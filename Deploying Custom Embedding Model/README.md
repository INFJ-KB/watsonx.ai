## IBM Watson Machine Learing을 사용하여 watsonx 플랫폼에 Custom Embedding Model 배포하기
watsonx.ai 플랫폼의 버전이 업그레이드되면서 고성능의 다양한 최신 모델들이 탑재되어 출시됩니다.<br>
그러나 다국어(한글) 지원, 비즈니스 도메인 특화된 영역에 대한 지원 등 경우에 따라서 기본 탑재된 모델이 이외에 사용자의 필요해 의해 수정된 커스텀 모델들을 플랫폼에 올려 서비스해야 하는 상황이 발생될 수 있습니다.<br>
watsonx.ai는 기업이 생성형 AI를 빠르게 적용하고, 확장할 수 있는 Enterprise AI 플랫폼으로써 다양한 상황에서 발생할 수 있는 기업 요구 사항들을 충족시킬 수 있도록 유연한 환경을 제공합니다.<br>

본 예제에서는 RAG(Retrieval-Augmented Generation) 구현 시 한글 embedding model로 활용되는 BAAI/bge-m3 모델을 Hugging Face에서 다운받아 watsonx.ai 플랫폼에 배포하여 사용하는 예제를 구현해 보도록 하겠습니다.<br>

### 관련 코드
- **Deploying custom embedding model** : Hugging Face에서 bge-m3 모델을 다운로드하고, Embedding Fuction을 작성하여 WML Deployment Space에 해당 Function을 Deploy하는 서버측 코드
  1. Hugging Face에서 bge-m3 모델을 다운로드합니다.
  2. Enbedding Function을 구현합니다.
  3. WML Deployment에 Function을 Deploy하기 위한 코드를 작성합니다.
  4. 모델을 Deploy합니다.
  5. 모델 서빙을 위한 End-Point URL이 생성됩니다.
- **Client App for calling custom embedding API** : End Point 로 노출된 Embedding API를 호출하여 원하는 Text를 bge-m3 모델로 embedding 하는 클라이언측 코드 
  1. End Point URL을 통해 Embedding API를 호출하여 text를 embedding 합니다.
  2. Embedding이 잘 되었는지 확인합니다. 

<br>

### 참고 자료
#### Deploying Python functions in Watson Machine Learning <br>
https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=assets-deploying-python-functions
#### The ibm-watsonx-ai library <br>
https://ibm.github.io/watsonx-ai-python-sdk/
