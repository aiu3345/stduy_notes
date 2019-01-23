# Spring Anotaions

- ## @Value annotaion

  - > properteis(지정된)  데이터에서 값을 불러와 변수에 지정할 때 사용

  - 일반적인 사용 형태 

  - ```java
    @Value("app.data")
    String data
    ```

    - 불러올 properties name 지정(app.data)
    - data에 해당 값 지정됨

  - jobparameter 형태 사용 (**Spring batch job** 수행 시)

    ```java
    @StepScope or @JobScope
    @Value("#{jobParameters['fileName']}"
    String fileName
    ```

    - Job 이나 step 중간에 job parameter 참조할 경우 사용