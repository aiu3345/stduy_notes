#### Optional 객체 

- 사용법 및 요약 

  - NPE(Null Pointer Exception) 을 방지하기 위해 사용 / 그에 관한 조건 Handling

  - before

    ```java
    String text = getText();
    int length;
    if (text != null) {
    	length = maybeText.get().length();
    } else {
    	length = 0;
    }
    ```

  - after

  - ```java
    int length = Optional.ofNullable(getText()).map(String::length).orElse(0);
    ```

    

- 적용 사례 관련 문서 (**강추**)
  - [1부](http://www.daleseo.com/java8-optional-before/)
  - [2부](http://www.daleseo.com/java8-optional-after/)
  - [3부](http://www.daleseo.com/java8-optional-before/)
- 참고 및 예제 링크 : [이동](https://medium.com/@joongwon/optional%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-java%EC%9D%98-nullpointerexception%EC%9D%84-%ED%94%BC%ED%95%B4%EB%B3%B4%EC%9E%90-e9cac719a2d6)