# Elastic Search Scroll API 

> 다량의 데이터를 iterate 하면서 데이터를 조회할 수 있게 하는 API
>
> 보통 배치성으로 수행되는 경우에 많이 쓰임 (전체 데이터를 rolling(paging) 해서 받아 오는 경우)



- ##### 수행과정 

  - 초기 사용 등록 

    - Scroll 인자 => timeunit: 1m(1 minute)) / 1번 scroll 수행 시 만료 시간
    - size & query  지정 후 호출

    ```java
    POST /twitter/_search?scroll=1m
    {
        "size": 100,
        "query": {
            "match" : {
                "title" : "elasticsearch"
            }
        }
    }
    ```

  - 이후 지속 호출 (완료 시 까지)

    - scroll_id는 최초 호출 시 반환됨
    - 최초 발급 후 완료 시까지 지속 사용  (Batch Job id가 발급되는 것과 비슷)

    ```json
    POST  /_search/scroll 
    {
        "scroll" : "1m", 
        "scroll_id" : "DXF1ZXJ5QW5kRmV0Y2gBAAAAAAAAAD4WYm9laVYtZndUQlNsdDcwakFMNjU1QQ==" 
    }
    ```

  - 사용 완료 후 삭제(클리어)

    - java 코드 방식 

    - ```java
      esClient.getClient().prepareClearScroll().addScrollId(scrollId).get().isSucceeded();
      ```

    - API 호출 

    - ```json
      DELETE /_search/scroll
      {
          "scroll_id" : "DXF1ZXJ5QW5kRmV0Y2gBAAAAAAAAAD4WYm9laVYtZndUQlNsdDcwakFMNjU1QQ=="
      }
      ```

      ```json
      DELETE /_search/scroll
      {
          "scroll_id" : [
            "DXF1ZXJ5QW5kRmV0Y2gBAAAAAAAAAD4WYm9laVYtZndUQlNsdDcwakFMNjU1QQ==",
            "DnF1ZXJ5VGhlbkZldGNoBQAAAAAAAAABFmtSWWRRWUJrU2o2ZExpSGJCVmQxYUEAAAAAAAAAAxZrUllkUVlCa1NqNmRMaUhiQlZkMWFBAAAAAAAAAAIWa1JZZFFZQmtTajZkTGlIYkJWZDFhQQAAAAAAAAAFFmtSWWRRWUJrU2o2ZExpSGJCVmQxYUEAAAAAAAAABBZrUllkUVlCa1NqNmRMaUhiQlZkMWFB"
          ]
      }
      ```

      

- ##### 특징

  - Keeping the Search Context Alive 특성 ([레퍼런스 링크](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-scroll.html#scroll-search-context))

- **참고 문서**
  - [공식 사이트](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-scroll.html)
  - [참고 블로그 1](http://www.kwangsiklee.com/2018/07/elasticsearch-%EC%97%90%EC%84%9C-scroll-api%EB%A1%9C-%EB%8C%80%EB%9F%89-%EC%B6%94%EC%B6%9C%ED%95%98%EA%B8%B0/)