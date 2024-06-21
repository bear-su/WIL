# Spring Security

## 스프링 시큐리티의 예외처리
`AuthenticationException`, `AccessDeniedException`와 같은 스프링 시큐리티 예외는 보통 authentication filter에서 발생하는 런타임 예외이다.
이런 인증 필터는 `DispatcherServlet` 또는 `Controller`에 동작하기 전에 위치하기 때문에 `ControllerAdvice`로 예외 처리를 할 수 없다.

따라서 예외처리를 하기 위해서는 커스텀 예외 핸들러 필터를 추가하고 응답 본문을 구성해야 한다. 이때 사용되는 구현체가 `AuthenticationEntryPoint`이다.
`AuthenticationEntryPoint`는 클라이언트에서 자격 증명을 요청하는 HTTP 응답을 보내는 데 사용된다.

## AuthenticationEntryPoint
- 사용자가 인증되지 않은 상태로 보호된 리소스에 접근하려고 할 때 호출되며, 사용자는 로그인 페이지로 리다이렉트되거나 401 Unauthorized 응답을 받게 된다. 
- 커스텀 AuthenticationEntryPoint를 구현하여 이 동작을 변경할 수 있다.

## AccessDeniedHandler
- 인증된 사용자가 특정 리소스에 접근하려고 할 때 필요한 권한이 없을 경우 호출되며, 기본적으로 403 Forbidden 응답을 반환한다.
- 커스텀 AccessDeniedHandler를 구현하여 다른 동작을 정의할 수 있다.



## 참고
- https://www.baeldung.com/spring-security-exceptionhandler