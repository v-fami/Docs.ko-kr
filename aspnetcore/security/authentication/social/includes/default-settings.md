**참고:** 에 대 한 호출 `AddIdentity` 기본 체계 설정을 구성 합니다. `AddAuthentication(string defaultScheme)` 집합 오버 로드는 `DefaultScheme` 속성 그 뿐만 아니라 `AddAuthentication(Action<AuthenticationOptions> configureOptions)` 만 명시적으로 설정 하는 속성을 설정 하는 오버 로드 합니다. 이러한 오버 로드 중 하나 에서만 호출 해야 한 번 추가 하는 경우 여러 인증 공급자. 에 대 한 후속 호출 이전에 구성 된 모든 재정의의 가능성이 있는 [AuthenticationOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.authenticationoptions) 속성입니다.