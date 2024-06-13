# 환경변수 파일로 관리하기.md


1. @PropertySources 어노테이션을 사용하여 외부 프로퍼티 파일을 로드한다. 
   - 스프링 컨테이너가 프로퍼티 파일을 읽어올 수 있도록 도와주는 어노테이션으로 스프링 컨테이너는 애플리케이션이 시작될 때 해당 파일을 읽어와 설정 정보를 로드한다.
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

2. yml 파일에 프로퍼티 파일의 경로를 설정한다.
   - 경로를 직접 명시해도 되지만 개발 환경, 운영 환경 등 환경 별로 설정하기 위함.
~~~yaml
property:
  path: classpath:properties/env-local.properties
~~~

3. 환경설정 파일 만들기 (`resources/properties` 디렉토리를 사용함) 
~~~properties
DATABASE_HOST=localhost:3306
DATABASE_USER=local
DATABASE_PASSWORD=localpassword
~~~

