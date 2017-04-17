---
title: "ASP.NET Core에서 웹 서버 구현이 WebListener | Microsoft 문서"
author: rick-anderson
description: "WebListener, ASP.NET 핵심 windows에 대 한 웹 서버를 소개합니다. Http.Sys 커널 모드 드라이버의 기술을 기반으로 한 WebListener는 IIS 없이 인터넷에 직접 연결에 사용할 수 있는 Kestrel 하지 않아도 됩니다."
keywords: "ASP.NET Core, WebListener, HttpListener, url 접두사 이며 SSL"
ms.author: riande
manager: wpickett
ms.date: 10/27/2016
ms.topic: article
ms.assetid: 0a7286e4-6428-424e-b5c4-5c98815cf61c
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/servers/weblistener
translationtype: Machine Translation
ms.sourcegitcommit: f93c93002fec0088a7040cd53f31fd5b5a62fea7
ms.openlocfilehash: 5c15094a35f1d998c01d4358904b7be6d92afdfd
ms.lasthandoff: 03/23/2017

---
# <a name="weblistener-web-server-implementation-in-aspnet-core"></a>ASP.NET Core에서 WebListener 웹 서버 구현

여 [Tom Dykstra](http://github.com/tdykstra) 및 [Chris Ross](https://github.com/Tratcher)

WebListener는는 [ASP.NET 핵심에 대 한 웹 서버](index.md) Windows 에서만 실행 하는 합니다. 기반으로 [Http.Sys 커널 모드 드라이버](https://msdn.microsoft.com/en-us/library/windows/desktop/aa364510.aspx)합니다. WebListener 하지 않아도 됩니다 [Kestrel](kestrel.md) 사용할 수 있는 인터넷에 직접 연결에 대 한 역방향 프록시 서버와 IIS에 의존 하지 않고 있습니다. 사실 **WebListener와 호환 되지 않습니다 IIS 또는 IIS Express를 사용할 수 없습니다는 [ASP.NET 핵심 모듈](aspnet-core-module.md)합니다.**

통해.NET Core 또는.NET Framework 응용 프로그램에서 직접 사용할 수 있지만 WebListener ASP.NET 핵심을 개발한는 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지입니다.

WebListener는 다음과 같은 기능을 지원합니다.

- Windows 인증 
- 포트 공유
- SNI에 대 한 HTTPS
- TLS (Windows 10)을 통해 HTTP/2
- 직접 파일 전송
- 응답 캐싱
- Websocket (Windows 8)

지원 되는 Windows 버전:

- Windows 7 및 Windows Server 2008 R2 이상

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)

## <a name="when-to-use-weblistener"></a>WebListener를 사용 하는 경우

WebListener는 IIS를 사용 하지 않고 인터넷에 직접 서버를 노출 해야 하는 배포에 유용 합니다.

![인터넷에 WebListener](weblistener/_static/weblistener-to-internet.png)

Http.Sys를 기반으로 하기 때문에 WebListener 공격 으로부터 보호에 대 한 역방향 프록시 서버를 필요 하지 않습니다. Http.Sys는 많은 종류의 공격 으로부터 보호 하 고 견고성, 보안 및 완전 한 기능의 웹 서버 확장성을 제공 하는 완성도 높은 기술 합니다. IIS 자체 Http.Sys 기반으로 하는 HTTP 수신기로 실행합니다. 

WebListener는 Kestrel를 사용 하 여 가져올 수 없습니다 제공 하는 기능 중 하나를 할 때 적합 한 내부 배포 이기도 합니다.

![인터넷에 WebListener](weblistener/_static/weblistener-to-internal.png)

## <a name="how-to-use-weblistener"></a>WebListener를 사용 하는 방법

호스트 OS와 ASP.NET 핵심 응용 프로그램에 대 한 설치 작업의 개요는 다음과 같습니다.

### <a name="configure-windows-server"></a>Windows Server를 구성 합니다.

* 응용 프로그램에 필요한와 같은.NET의 버전을 설치 [.NET Core](https://go.microsoft.com/fwlink/?LinkID=827524) 또는.NET Framework 4.5.1입니다.

* WebListener에 바인딩하고 SSL 인증서를 설정에 대 한 URL 접두사를 미리 등록

   Windows의 URL 접두사를 미리 등록 하지 경우 관리자 권한으로 응용 프로그램을 실행 해야 합니다. 유일한 예외는 포트 번호가; 1024 보다 큰 HTTP (HTTPS)을 사용 하 여 localhost에 바인딩할 경우 이 경우 관리자 권한을 사용할 필요가 없습니다.

   자세한 내용은 다음을 참조 하십시오. [미리 접두사를 등록 하 고 SSL을 구성 하는 방법](#preregister-url-prefixes-and-configure-ssl) 이 문서의 뒷부분에 나오는 합니다.

* WebListener 도달 하는 트래픽을 허용 하도록 방화벽 포트를 엽니다.

   Netsh.exe를 사용 하면 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)합니다.

이 밖에도 [Http.Sys 레지스트리 설정](https://support.microsoft.com/en-us/kb/820129)합니다.

### <a name="configure-your-aspnet-core-application"></a>ASP.NET 핵심 응용 프로그램 구성

* NuGet 패키지 설치 [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/)합니다. 도 설치 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) 종속성으로 합니다.

* 호출의 [ `UseWebListener` ](http://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNetCore/Hosting/WebHostBuilderKestrelExtensions/index.html#Microsoft.AspNetCore.Hosting.WebHostBuilderWebListenerExtensions.UseWebListener.md) 대 한 확장 메서드 [WebHostBuilder](http://docs.asp.net/projects/api/en/latest/autoapi/Microsoft/AspNetCore/Hosting/WebHostBuilder/index.html#Microsoft.AspNetCore.Hosting.WebHostBuilder.md) 에 프로그램 `Main` 모든 WebListener를 지정 하는 메서드를 [옵션](https://github.com/aspnet/WebListener/blob/dev/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) 및 [설정을](https://github.com/aspnet/WebListener/blob/dev/src/Microsoft.Net.Http.Server/WebListenerSettings.cs) 는 다음 예제와 같이 필요한:

  [!code-csharp[](weblistener/sample/Program.cs?name=snippet_Main&highlight=13-17)]

* Url 및 포트에서 수신 하도록 구성 

  ASP.NET 핵심이 바인딩됩니다 기본적으로 `http://localhost:5000`합니다. URL 접두사와 포트를 구성 하려면 사용할 수는 `UseURLs` 확장 메서드는 `urls` 명령줄 인수 또는 ASP.NET 핵심 구성 시스템. 자세한 내용은 참조 [호스팅](../../fundamentals/hosting.md)합니다.

  수신기 사용 하 여 웹의 [Http.Sys 접두사 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)합니다. 요구 사항이 없습니다 접두사 문자열 형식 WebListener 관련 된입니다.

  > [!NOTE]
  > 동일한 접두사 문자열을 지정 해야 `UseUrls` 하는 서버에서 미리 등록 합니다. 

* 응용 프로그램은 IIS 또는 IIS Express를 실행 하도록 구성 되지 있는지 확인 합니다.

  Visual Studio에서 IIS Express에 대 한 기본 실행 프로필은입니다.  콘솔 응용 프로그램 프로젝트를 실행 하려면 수동으로 변경 해야 선택한 프로 파일에서는 다음 스크린 샷과 같이 합니다.

  ![콘솔 응용 프로그램 프로필을 선택 합니다.](weblistener/_static/vs-choose-profile.png)

## <a name="how-to-use-weblistener-outside-of-aspnet-core"></a>ASP.NET Core 외부 WebListener를 사용 하는 방법

* 설치는 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지입니다.

* [WebListener에 바인딩하고 SSL 인증서를 설정에 대 한 URL 접두사를 미리 등록](#preregister-url-prefixes-and-configure-ssl) ASP.NET 코어에서 사용 하기 위해와 마찬가지로 합니다.

이 밖에도 [Http.Sys 레지스트리 설정](https://support.microsoft.com/en-us/kb/820129)합니다.


ASP.NET Core 외부에서 WebListener 사용을 보여 주는 코드 예제는 다음과 같습니다.

```csharp
var settings = new WebListenerSettings();
settings.UrlPrefixes.Add("http://localhost:8080");

using (WebListener listener = new WebListener(settings))
{
    listener.Start();

    while (true)
    {
        var context = await listener.AcceptAsync();
        byte[] bytes = Encoding.ASCII.GetBytes("Hello World: " + DateTime.Now);
        context.Response.ContentLength = bytes.Length;
        context.Response.ContentType = "text/plain";

        await context.Response.Body.WriteAsync(bytes, 0, bytes.Length);
        context.Dispose();
    }
}
```

## <a name="preregister-url-prefixes-and-configure-ssl"></a>URL 접두사를 미리 등록 하 고 SSL 구성

IIS와 WebListener 기본 Http.Sys 커널 모드 드라이버에 요청을 수신 하 고 초기 처리를 수행 합니다. Iis에서 관리 UI 하면 모든 항목을 구성 하는 비교적 쉬운 방법이 있습니다. 그러나 WebListener를 사용 하는 경우 사용자가 직접 Http.Sys를 구성 해야 합니다. 즉 netsh.exe를 수행 하기 위한 기본 제공 도구입니다. 

에 대 한 netsh.exe를 사용 해야 하는 가장 일반적인 작업은 URL 접두사를 예약 및 SSL 인증서를 할당 합니다.

NetSh.exe는 초보자를 위한 사용 하기 편리한 도구 않습니다. 다음 예제에서는 포트 80 및 443에 대 한 URL 접두사를 예약 하는 데 필요한 최소 코드를 보여 줍니다.

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

다음 예제에는 SSL 인증서를 할당 하는 방법을 보여 줍니다.

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}".
```

공식 참조 설명서는 다음과 같습니다.

* [Netsh 명령은 하이퍼텍스트 전송 프로토콜 (HTTP)](http://technet.microsoft.com/library/cc725882.aspx)
* [UrlPrefix 문자열](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

다음 리소스는 몇 가지 시나리오에 대 한 자세한 지침을 제공 합니다. 문서를 참조 하는 `HttpListener` 에 동일 하 게 적용 `WebListener`와 마찬가지로 모두 Http.Sys를 기반으로 합니다.

* [방법: SSL 인증서로 포트 구성](http://msdn.microsoft.com/library/ms733791.aspx)
* [HTTPS 통신-HttpListener 기반 호스팅 및 클라이언트 인증](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) 이 제 블로그 비교적 오래 된 하지만 유용한 정보가 여전히 포함 되어 있습니다.
* [방법: 연습을 사용 하 여 HttpListener 또는 Http 서버 비관리 코드 (c + +)를 SSL 간단한 서버로](http://blogs.msdn.com/b/jpsanders/archive/2009/09/29/walkthrough-using-httplistener-as-an-ssl-simple-server.aspx) 이 점 역시 유용한 정보로는 오래 된 블로그입니다.
* [SSL과 함께.NET Core WebListener 설정 방법](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)

다음은 netsh.exe 명령줄 보다 쉽게 사용할 수 있는 몇 가지 타사 도구입니다. 제공 하 되거나 Microsoft에서 보증 되지 않은 이러한 합니다. 도구 자체 netsh.exe에 대 한 관리자 권한이 필요 하므로 관리자 권한으로 기본적으로 실행 합니다.

* [HttpSysManager](http://httpsysmanager.codeplex.com/) 목록에 대 한 UI를 제공 하 고 예약을 접두사 및 인증서 신뢰 목록이 SSL 인증서 및 옵션을 구성 합니다. 
* [HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx) 나열 하거나 SSL 인증서와 URL 접두사를 구성할 수 있습니다. UI는 HttpSysManager 보다 성능이 우수 하 고 몇 가지 추가 구성 옵션을 노출 하지만 그렇지 않으면 비슷한 기능을 제공 합니다. 그 새 인증서 신뢰 목록 (CTL)를 만들 수는 없지만 기존 노트북을 할당할 수 있습니다.

Microsoft 자체 서명 된 SSL 인증서를 생성 하기 위한 명령줄 도구를 제공 합니다. [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) 및 PowerShell cmdlet [새로 SelfSignedCertificate](https://technet.microsoft.com/library/hh848633)합니다. 자체 서명 된 SSL 인증서를 생성 하 여 쉽게 해 주는 타사 UI 도구도 있습니다.

* [SelfCert](https://www.pluralsight.com/blog/software-development/selfcert-create-a-self-signed-certificate-interactively-gui-or-programmatically-in-net)
* [Makecert UI](http://makecertui.codeplex.com/)

## <a name="next-steps"></a>다음 단계

자세한 내용은 다음 리소스를 참조하세요.

* [이 문서에 대 한 샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)
* [WebListener 소스 코드](https://github.com/aspnet/WebListener)
* [호스팅](../hosting.md)
