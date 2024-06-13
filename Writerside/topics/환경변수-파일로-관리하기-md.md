# 환경변수 파일로 관리하기.md

- @PropertySources를 이용해서 이를 달성할 수 있다.
```Java
@PropertySources({
        @PropertySource("${property.path}")
})
@SpringBootApplication
public class FivestarBackendApplication {

    public static void main(String[] args) {
        SpringApplication.run(FivestarBackendApplication.class, args);
    }

}
```

- yml 파일에 경로 설정
~~~yaml
property:
  path: classpath:properties/env-local.properties
~~~

- resources/properties/env-local.properties 파일 만들기
~~~properties
DATABASE_HOST=localhost:3306
DATABASE_USER=local
DATABASE_PASSWORD=localpassword
~~~