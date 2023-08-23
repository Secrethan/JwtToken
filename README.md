# Security + JWT
<b>스프링 시큐리티에서 제공하는 필터 변경</b>
1. usernamePasswordAuthenticationFilter
   * attemptAuthentication() : 요청 정보 중 id, password를 토대로 인증을 위한 토큰 생성 후 AuthenticationManager를 통해 인증
   * 변경 사항<br>
     * 요청 정보를 json 형태로 받아 DTO 파싱 <br><br>
   * successfulAuthentication() : 주로 세션 관리나 인증 정보 생성, 로그 기록 등을 수행
   * 변경 사항<br>
     * JWT 토큰 생성
     * 응답 헤더에 토큰 담아 클라이언트로 보냄 <br><br>

2. BasicAuthenticationFilter
   * doFilterInternal() : 클라이언트의 요청 중 인증, 권한 부여가 필요한 요청이 발생하면 이를 검증하고 다음 필터 체인을 호출
   * 변경 사항<br>
     * 요청 헤더에서 Jwt 토큰 정보를 추출, 검증
     * 검증에 성공하면 해당 유저 정보를 토대로 Authenticaion 객체를 세션에 저장
     * 세션이 종료되기 전까지 인증 정보 유지 
