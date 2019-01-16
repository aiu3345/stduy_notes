# Elastic Search

- ### 정의
   ```
   확장성이 뛰어난(highly scalable) full-text 분산 검색 및 분석 엔진으로 거의 실시간(Near-Real Time)로 큰 볼륨의 데이터를 저장하고, 분석하고 검색할 수있다.
   ```

- ### 특징

  - **Schemaless / Document-Oriented**

    ```
    사전에 정의한 스키마 나 기준 필요 없이 검색 문서 기준(Document-Oriented) 동적인 열과 데이터 타입 형태의 입력을 지원
    ```

  - **검색**
    ```
    텍스트 검색, 특히 Full-Text 검색에 특화되어 있으며, 각각의 용어 분석(형태소 분석 후 Lucene 색인)하여 최적화하는 것도 가능하다.
    ```

  - **분석**

    ```
    다양한 환경에서 분석 도구로 사용 가능하며
    분석을 위해 폭 넓고 다양한 집계(Aggregation) 기능을 지원 다양한 데이터 타입에 적용 가능
    ```

  - **풍부한 클라이언트 라이브러리 및 Rest API**

    ```
    * 다양한 프로그래밍 언어에서 사용할 수 있도록 클라이언트 라이브러리를 제공한다.
      (## Java, C# Python, PHP, Perl, Ruby 등)
    * REST(Representational State Transfer) API로 다양한 제어가 가능하다
    * 참고문서-Elastic Search Rest API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs.html)
    ```

  - **운영 및 확장 용이**

    ```
    단일 노드 운영 뿐만아니라 수백개의 노드까지도 수평적 손쉽게 확장(Horizontal Scalability) 가능하도록 되어있다. 성능이 향상에 비용이 많이드는 단일 서버보다 수십,수백대의 저렴한 서버로 구성 가능하며, 노드 추가 또한 간단하다.
    ```

  - **NRT(Near-Real Time)**

    ```markdown
    데이터(문서) 저장 및 색인 후 거의 1초 이내에 쿼리를 통해 확인 가능하며 초당 수백~수천개의 도큐먼트 색인 생성하고 거의 실시간(Near-RealTime)으로 검색할 수 있다.
    ```

  - **신속성**

    ```
    Apache luncene 기반으로 구성되어 최적화 및 색인 속도가 빠르다.
    ```

  - **Fault tolerant (결함 허용성)**

    ```
    노드 및 네트워크 장애와 같은 하드웨어 장애 상황에서도 계속 실행할 수 있으며, 장애 발생 시 장애가 발생한 노드에서 다른 활성화 노드로 복제해, 클러스터를 계속 운용 가능하다.
    ```


- ### Elastic Search 설치 및 실행

   ```shell
   # curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.5.4.tar.gz
   # tar xvzf elasticsearch-6.5.4.tar.gz
   # cd elasticsearch-6.5.4
   # bin/elasticsearch
   ```

   결과

   ```json
   # curl http://localhost:9200
{
    "name" : "node-1",
    "cluster_name" : "my-application",
    "cluster_uuid" : "-Gd4MgKHTnK8nefmwkWtnw",
    "version" : {
    "number" : "6.5.4",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "d2ef93d",
    "build_date" : "2018-12-17T21:17:40.758843Z",
    "build_snapshot" : false,
    "lucene_version" : "7.5.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
    },
    "tagline" : "You Know, for Search"
}
   ```



# Kibana
- ### 정의
   ```
   - Elastic Search 데이터에서 통찰력을 얻는데 도움주는 Elastic Stack의 시각화 도구
   - 막대그래프, 지도, 선형 차트, 시계열 등 다양한 시각화 기능 제공
   - REST API 요청 작성 및 테스트할 수 있는 기능 제공
   ```

- ### Kibana 설치 및 실행
   - 다운로드 및 압축 풀기

   ```shell
   # curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-6.5.4-darwin-x86_64.tar.gz
   # tar xvzf kibana-6.5.4-darwin-x86_64.tar.gz
   ```
   - config 수정
   ```shell
   # cd kibana-6.5.4-darwin-x86_64
   # vim config/kibana.yml
   ```
   ```bash
   ## port 정보 수정 (default: 5601)
   server.port: 5601
   ## kibana meta 정보 저장할 elasticsearch 정보 등록
   ## default (http://localhost:9200)
   elasticsearch.url="http://localhost:9200"
   ```
   - 실행
   ```shell
   # cd kibana-6.5.4-darwin-x86_64
   # bin/kibana
   ```
   -  결과
     ![kibna 실행](.\img\kibana_run.png)
