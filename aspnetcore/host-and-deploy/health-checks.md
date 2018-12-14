---
title: ASP.NET Core의 상태 검사
author: guardrex
description: 앱 및 데이터베이스와 같은 ASP.NET Core 인프라의 상태 검사를 설정하는 방법에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 12/03/2018
uid: host-and-deploy/health-checks
ms.openlocfilehash: d8fd43d9d689396cf30ca371763cdf7ac9423c77
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862632"
---
# <a name="health-checks-in-aspnet-core"></a><span data-ttu-id="87c28-103">ASP.NET Core의 상태 검사</span><span class="sxs-lookup"><span data-stu-id="87c28-103">Health checks in ASP.NET Core</span></span>

<span data-ttu-id="87c28-104">[Luke Latham](https://github.com/guardrex) 및 [Glenn Condron](https://github.com/glennc) 기준</span><span class="sxs-lookup"><span data-stu-id="87c28-104">By [Luke Latham](https://github.com/guardrex) and [Glenn Condron](https://github.com/glennc)</span></span>

<span data-ttu-id="87c28-105">ASP.NET Core는 앱 인프라 구성 요소의 상태를 보고하기 위해 상태 검사 미들웨어와 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-105">ASP.NET Core offers Health Check Middleware and libraries for reporting the health of app infrastructure components.</span></span>

<span data-ttu-id="87c28-106">상태 검사는 앱에 의해 HTTP 엔드포인트로서 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-106">Health checks are exposed by an app as HTTP endpoints.</span></span> <span data-ttu-id="87c28-107">상태 검사 엔드포인트는 다양한 실시간 모니터링 시나리오에 맞게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-107">Health check endpoints can be configured for a variety of real-time monitoring scenarios:</span></span>

* <span data-ttu-id="87c28-108">상태 프로브는 컨테이너 오케스트레이터와 부하 분산 장치가 앱 상태를 검사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-108">Health probes can be used by container orchestrators and load balancers to check an app's status.</span></span> <span data-ttu-id="87c28-109">예를 들어, 컨테이너 오케스트레이터는 롤링 배포를 중지하거나 컨테이너를 다시 시작하여 실패한 상태 검사에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-109">For example, a container orchestrator may respond to a failing health check by halting a rolling deployment or restarting a container.</span></span> <span data-ttu-id="87c28-110">부하 분산 장치는 장애가 발생한 상태 검사 인스턴스로부터 트래픽을 다른 곳으로 라우팅하여 비정상 앱에 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-110">A load balancer might react to an unhealthy app by routing traffic away from the failing instance to a healthy instance.</span></span>
* <span data-ttu-id="87c28-111">메모리, 디스크 및 기타 물리적 서버 리소스의 사용이 정상적인 상태인지 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-111">Use of memory, disk, and other physical server resources can be monitored for healthy status.</span></span>
* <span data-ttu-id="87c28-112">상태 검사는 데이터베이스 및 외부 서비스 엔드포인트와 같은 앱 종속성을 테스트하여 가용성 및 정상 작동 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-112">Health checks can test an app's dependencies, such as databases and external service endpoints, to confirm availability and normal functioning.</span></span>

<span data-ttu-id="87c28-113">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="87c28-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/health-checks/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="87c28-114">샘플 앱에는 이 항목에 설명된 시나리오의 예가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-114">The sample app includes examples of the scenarios described in this topic.</span></span> <span data-ttu-id="87c28-115">지정된 시나리오에 대해 샘플 앱을 실행하려면 명령 셸의 프로젝트 폴더에서 [dotnet run](/dotnet/core/tools/dotnet-run) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-115">To run the sample app for a given scenario, use the [dotnet run](/dotnet/core/tools/dotnet-run) command from the project's folder in a command shell.</span></span> <span data-ttu-id="87c28-116">샘플 앱의 사용 방법에 대한 자세한 내용은 샘플 앱의 *README.md* 파일과 이 항목의 시나리오 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87c28-116">See the sample app's *README.md* file and the scenario descriptions in this topic for details on how to use the sample app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87c28-117">전제 조건</span><span class="sxs-lookup"><span data-stu-id="87c28-117">Prerequisites</span></span>

<span data-ttu-id="87c28-118">상태 검사는 일반적으로 외부 모니터링 서비스 또는 컨테이너 오케스트레이터와 함께 사용되어 앱 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-118">Health checks are usually used with an external monitoring service or container orchestrator to check the status of an app.</span></span> <span data-ttu-id="87c28-119">앱에 상태 검사를 추가하기 전에 사용할 모니터링 시스템을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-119">Before adding health checks to an app, decide on which monitoring system to use.</span></span> <span data-ttu-id="87c28-120">모니터링 시스템은 어떤 유형의 상태 검사를 만들고 그 엔드포인트를 구성하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-120">The monitoring system dictates what types of health checks to create and how to configure their endpoints.</span></span>

<span data-ttu-id="87c28-121">[Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)를 참조하거나 [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) 패키지에 대한 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-121">Reference the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) or add a package reference to the [Microsoft.AspNetCore.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.HealthChecks) package.</span></span>

<span data-ttu-id="87c28-122">샘플 앱은 여러 시나리오의 상태 검사를 보여주는 시작 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-122">The sample app provides start-up code to demonstrate health checks for several scenarios.</span></span> <span data-ttu-id="87c28-123">[데이터베이스 프로브](#database-probe) 시나리오는 [BeatPulse](https://github.com/Xabaril/BeatPulse)를 사용하여 데이터베이스 연결의 상태를 프로브합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-123">The [database probe](#database-probe) scenario probes the health of a database connection using [BeatPulse](https://github.com/Xabaril/BeatPulse).</span></span> <span data-ttu-id="87c28-124">[DbContext 프로브](#entity-framework-core-dbcontext-probe) 시나리오는 EF Core `DbContext`를 사용하여 데이터베이스를 프로브합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-124">The [DbContext probe](#entity-framework-core-dbcontext-probe) scenario probes a database using an EF Core `DbContext`.</span></span> <span data-ttu-id="87c28-125">샘플 앱을 사용하여 데이터베이스 시나리오를 탐색하려면 다음을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="87c28-125">To explore the database scenarios using the sample app:</span></span>

* <span data-ttu-id="87c28-126">데이터베이스를 만들고 앱의 *appsettings.json* 파일에서 연결 문자열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-126">Create a database and provide its connection string in the *appsettings.json* file of the app.</span></span>
* <span data-ttu-id="87c28-127">[AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/)에 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-127">Add a package reference to [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/).</span></span>

> [!NOTE]
> <span data-ttu-id="87c28-128">[BeatPulse](https://github.com/Xabaril/BeatPulse)는 Microsoft에서 유지 관리하거나 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-128">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

<span data-ttu-id="87c28-129">다른 상태 검사 시나리오는 관리 포트에 대해 상태 검사를 필터링하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-129">Another health check scenario demonstrates how to filter health checks to a management port.</span></span> <span data-ttu-id="87c28-130">샘플 앱을 사용하려면 관리 URL과 관리 포트가 포함된 *Properties/launchSettings.json*  파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-130">The sample app requires you to create a *Properties/launchSettings.json* file that includes the management URL and management port.</span></span> <span data-ttu-id="87c28-131">자세한 내용은 [포트별 필터링](#filter-by-port) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87c28-131">For more information, see the [Filter by port](#filter-by-port) section.</span></span>

## <a name="basic-health-probe"></a><span data-ttu-id="87c28-132">기본 상태 프로브</span><span class="sxs-lookup"><span data-stu-id="87c28-132">Basic health probe</span></span>

<span data-ttu-id="87c28-133">많은 앱의 경우, 요청을 처리할 수 있는 앱의 가용성(*활동성*)을 보고하는 기본 상태 검사 구성으로 앱 상태를 충분히 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-133">For many apps, a basic health probe configuration that reports the app's availability to process requests (*liveness*) is sufficient to discover the status of the app.</span></span>

<span data-ttu-id="87c28-134">기본 구성은 상태 검사 서비스를 등록하고 상태 검사 미들웨어를 호출하여 URL 엔드포인트에서 상태 응답을 사용하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-134">The basic configuration registers health check services and calls the Health Check Middleware to respond at a URL endpoint with a health response.</span></span> <span data-ttu-id="87c28-135">기본적으로 특정 종속성이나 하위 시스템을 테스트하기 위해 특정 상태 검사가 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-135">By default, no specific health checks are registered to test any particular dependency or subsystem.</span></span> <span data-ttu-id="87c28-136">상태 엔드포인트 URL에서 응답할 수 있는 경우 앱 상태가 좋은 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-136">The app is considered healthy if it's capable of responding at the health endpoint URL.</span></span> <span data-ttu-id="87c28-137">기본 응답 기록기는 상태(`HealthCheckStatus`)를 클라이언트에 대한 일반 텍스트 응답으로 기록하여 `HealthCheckResult.Healthy` 또는 `HealthCheckResult.Unhealthy` 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-137">The default response writer writes the status (`HealthCheckStatus`) as a plaintext response back to the client, indicating either a `HealthCheckResult.Healthy` or `HealthCheckResult.Unhealthy` status.</span></span>

<span data-ttu-id="87c28-138">`Startup.ConfigureServices`의 `AddHealthChecks`에 상태 검사 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-138">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="87c28-139">`Startup.Configure`의 요청 처리 파이프라인에 있는 `UseHealthChecks`로 상태 검사 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-139">Add Health Check Middleware with `UseHealthChecks` in the request processing pipeline of `Startup.Configure`.</span></span>

<span data-ttu-id="87c28-140">샘플 앱에서 상태 검사 엔드포인트는 `/health`(*BasicStartup.cs*)에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-140">In the sample app, the health check endpoint is created at `/health` (*BasicStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/BasicStartup.cs?name=snippet1&highlight=5,10)]

<span data-ttu-id="87c28-141">샘플 앱을 사용하여 기본 구성 시나리오를 실행하려면 명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-141">To run the basic configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario basic
```

### <a name="docker-example"></a><span data-ttu-id="87c28-142">Docker 예</span><span class="sxs-lookup"><span data-stu-id="87c28-142">Docker example</span></span>

<span data-ttu-id="87c28-143">[Docker](xref:host-and-deploy/docker/index)는 기본 상태 검사 구성을 사용하는 앱의 상태를 검사하는 데 사용할 수 있는 기본 제공 `HEALTHCHECK` 지시문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-143">[Docker](xref:host-and-deploy/docker/index) offers a built-in `HEALTHCHECK` directive that can be used to check the status of an app that uses the basic health check configuration:</span></span>

```
HEALTHCHECK CMD curl --fail http://localhost:5000/health || exit
```

## <a name="create-health-checks"></a><span data-ttu-id="87c28-144">상태 검사 만들기</span><span class="sxs-lookup"><span data-stu-id="87c28-144">Create health checks</span></span>

<span data-ttu-id="87c28-145">상태 검사는 `IHealthCheck` 인터페이스를 구현하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-145">Health checks are created by implementing the `IHealthCheck` interface.</span></span> <span data-ttu-id="87c28-146">`IHealthCheck.CheckHealthAsync` 메서드는 상태를 `Healthy`, `Degraded` 또는 `Unhealthy`로 나타내는 `Task<HealthCheckResult>`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-146">The `IHealthCheck.CheckHealthAsync` method returns a `Task<HealthCheckResult>` that indicates the health as `Healthy`, `Degraded`, or `Unhealthy`.</span></span> <span data-ttu-id="87c28-147">결과는 구성 가능한 상태 코드가 있는 일반 텍스트 응답으로 기록됩니다(구성은 [상태 검사 옵션](#health-check-options) 섹션에 설명되어 있음).</span><span class="sxs-lookup"><span data-stu-id="87c28-147">The result is written as a plaintext response with a configurable status code (configuration is described in the [Health check options](#health-check-options) section).</span></span> <span data-ttu-id="87c28-148">`HealthCheckResult`는 선택 사항인 키-값 쌍을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-148">`HealthCheckResult` can also return optional key-value pairs.</span></span>

### <a name="example-health-check"></a><span data-ttu-id="87c28-149">상태 검사 예</span><span class="sxs-lookup"><span data-stu-id="87c28-149">Example health check</span></span>

<span data-ttu-id="87c28-150">다음 `ExampleHealthCheck` 클래스는 상태 검사의 레이아웃을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-150">The following `ExampleHealthCheck` class demonstrates the layout of a health check:</span></span>

```csharp
public class ExampleHealthCheck : IHealthCheck
{
    public ExampleHealthCheck()
    {
        // Use dependency injection (DI) to supply any required services to the
        // health check.
    }

    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context, 
        CancellationToken cancellationToken = default(CancellationToken))
    {
        // Execute health check logic here. This example sets a dummy
        // variable to true.
        var healthCheckResultHealthy = true;

        if (healthCheckResultHealthy)
        {
            return Task.FromResult(
                HealthCheckResult.Healthy("The check indicates a healthy result."));
        }

        return Task.FromResult(
            HealthCheckResult.Unhealthy("The check indicates an unhealthy result."));
    }
}
```

### <a name="register-health-check-services"></a><span data-ttu-id="87c28-151">상태 검사 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="87c28-151">Register health check services</span></span>

<span data-ttu-id="87c28-152">`ExampleHealthCheck` 형식은 `AddCheck`으로 상태 검사 서비스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-152">The `ExampleHealthCheck` type is added to health check services with `AddCheck`:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck<ExampleHealthCheck>("example_health_check");
}
```

<span data-ttu-id="87c28-153">다음 예제에 표시된 `AddCheck` 오버로드는 상태 검사에서 오류가 보고되면 보고하도록 오류 상태(`HealthStatus`)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-153">The `AddCheck` overload shown in the following example sets the failure status (`HealthStatus`) to report when the health check reports a failure.</span></span> <span data-ttu-id="87c28-154">오류 상태가 `null`(기본값)로 설정되면 `HealthStatus.Unhealthy`가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-154">If the failure status is set to `null` (default), `HealthStatus.Unhealthy` is reported.</span></span> <span data-ttu-id="87c28-155">이 오버로드는 라이브러리 작성자에게 유용한 시나리오입니다. 이 라이브러리에서는 상태 검사 구현이 설정을 준수하는 경우 상태 검사 실패가 발생할 때 라이브러리가 나타내는 오류 상태는 앱에 의해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-155">This overload is a useful scenario for library authors, where the failure status indicated by the library is enforced by the app when a health check failure occurs if the health check implementation honors the setting.</span></span>

<span data-ttu-id="87c28-156">*태그*를 사용하여 상태 검사를 필터링할 수 있습니다([필터 상태 검사](#filter-health-checks) 섹션에 자세히 설명되어 있음).</span><span class="sxs-lookup"><span data-stu-id="87c28-156">*Tags* can be used to filter health checks (described further in the [Filter health checks](#filter-health-checks) section).</span></span>

```csharp
services.AddHealthChecks()
    .AddCheck<ExampleHealthCheck>(
        "example_health_check", 
        failureStatus: HealthStatus.Degraded, 
        tags: new[] { "example" });
```

<span data-ttu-id="87c28-157">`AddCheck`는 람다 함수를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-157">`AddCheck` can also execute a lambda function.</span></span> <span data-ttu-id="87c28-158">다음 예제에서 상태 검사 이름은 `Example`로 지정되고 검사는 항상 정상 상태를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-158">In the following example, the health check name is specified as `Example` and the check always returns a healthy state:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Example", () => 
            HealthCheckResult.Healthy("Example is OK!"), tags: new[] { "example" })
}
```

### <a name="use-health-checks-middleware"></a><span data-ttu-id="87c28-159">상태 검사 미들웨어 사용</span><span class="sxs-lookup"><span data-stu-id="87c28-159">Use Health Checks Middleware</span></span>

<span data-ttu-id="87c28-160">`Startup.Configure`에서 엔드포인트 URL 또는 상대 경로를 사용하여 처리 파이프라인에서 `UseHealthChecks`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-160">In `Startup.Configure`, call `UseHealthChecks` in the processing pipeline with the endpoint URL or relative path:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health");
}
```

<span data-ttu-id="87c28-161">상태 검사가 특정 포트에서 수신 대기해야 하는 경우 `UseHealthChecks`의 오버로드를 사용하여 포트를 설정합니다([포트별 필터링 ](#filter-by-port) 섹션에 자세히 설명되어 있음).</span><span class="sxs-lookup"><span data-stu-id="87c28-161">If the health checks should listen on a specific port, use an overload of `UseHealthChecks` to set the port (described further in the [Filter by port](#filter-by-port) section):</span></span>

```csharp
app.UseHealthChecks("/health", port: 8000);
```

<span data-ttu-id="87c28-162">상태 검사 미들웨어는 앱의 요청 처리 파이프라인에 있는 *터미널 미들웨어*입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-162">Health Checks Middleware is a *terminal middleware* in the app's request processing pipeline.</span></span> <span data-ttu-id="87c28-163">요청 URL과 정확히 일치하는 첫 번째 상태 검사 엔드포인트가 실행되고 나머지 미들웨어 파이프라인을 단락합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-163">The first health check endpoint encountered that's an exact match to the request URL executes and short-circuits the rest of the middleware pipeline.</span></span> <span data-ttu-id="87c28-164">단락이 발생하면 일치하는 상태 검사 이후 미들웨어는 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-164">When short-circuiting occurs, no middleware following the matched health check executes.</span></span>

## <a name="health-check-options"></a><span data-ttu-id="87c28-165">상태 검사 옵션</span><span class="sxs-lookup"><span data-stu-id="87c28-165">Health check options</span></span>

<span data-ttu-id="87c28-166">`HealthCheckOptions`는 다음과 같은 상태 검사 동작을 사용자 지정할 수 있는 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-166">`HealthCheckOptions` provide an opportunity to customize health check behavior:</span></span>

* [<span data-ttu-id="87c28-167">상태 검사 필터링</span><span class="sxs-lookup"><span data-stu-id="87c28-167">Filter health checks</span></span>](#filter-health-checks)
* [<span data-ttu-id="87c28-168">HTTP 상태 코드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="87c28-168">Customize the HTTP status code</span></span>](#customize-the-http-status-code)
* [<span data-ttu-id="87c28-169">캐시 헤더 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="87c28-169">Suppress cache headers</span></span>](#suppress-cache-headers)
* [<span data-ttu-id="87c28-170">출력 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="87c28-170">Customize output</span></span>](#customize-output)

### <a name="filter-health-checks"></a><span data-ttu-id="87c28-171">상태 검사 필터링</span><span class="sxs-lookup"><span data-stu-id="87c28-171">Filter health checks</span></span>

<span data-ttu-id="87c28-172">기본적으로 상태 검사 미들웨어는 등록된 모든 상태 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-172">By default, Health Check Middleware runs all registered health checks.</span></span> <span data-ttu-id="87c28-173">상태 검사 하위 세트를 실행하려면 `Predicate` 옵션에 부울 값을 반환하는 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-173">To run a subset of health checks, provide a function that returns a boolean to the `Predicate` option.</span></span> <span data-ttu-id="87c28-174">다음 예제에서는 상태 검사의 `Tag` 속성이 `foo_tag` 또는 `baz_tag`와 일치하는 경우에만 `true`가 반환되는 함수의 조건문에서 태그(`bar_tag`)에 의해 `Bar` 상태 검사가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-174">In the following example, the `Bar` health check is filtered out by its tag (`bar_tag`) in the function's conditional statement, where `true` is only returned if the health check's `Tag` property matches `foo_tag` or `baz_tag`:</span></span>

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void ConfigureServices(IServiceCollection services)
{
    services.AddHealthChecks()
        .AddCheck("Foo", () => 
            HealthCheckResult.Healthy("Foo is OK!"), tags: new[] { "foo_tag" })
        .AddCheck("Bar", () => 
            HealthCheckResult.Unhealthy("Bar is unhealthy!"), tags: new[] { "bar_tag" })
        .AddCheck("Baz", () => 
            HealthCheckResult.Healthy("Baz is OK!"), tags: new[] { "baz_tag" });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // Filter out the 'Bar' health check. Only Foo and Baz execute.
        Predicate = (check) => check.Tags.Contains("foo_tag") || 
            check.Tags.Contains("baz_tag")
    });
}
```

### <a name="customize-the-http-status-code"></a><span data-ttu-id="87c28-175">HTTP 상태 코드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="87c28-175">Customize the HTTP status code</span></span>

<span data-ttu-id="87c28-176">`ResultStatusCodes`를 사용하여 상태를 HTTP 상태 코드에 매핑하는 작업을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-176">Use `ResultStatusCodes` to customize the mapping of health status to HTTP status codes.</span></span> <span data-ttu-id="87c28-177">다음 `StatusCode` 할당은 미들웨어에서 사용되는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-177">The following `StatusCode` assignments are the default values used by the middleware.</span></span> <span data-ttu-id="87c28-178">요구 사항에 맞게 상태 코드 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-178">Change the status code values to meet your requirements.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The following StatusCodes are the default assignments for
        // the HealthCheckStatus properties.
        ResultStatusCodes =
        {
            [HealthCheckStatus.Healthy] = StatusCodes.Status200OK,
            [HealthCheckStatus.Degraded] = StatusCodes.Status200OK,
            [HealthCheckStatus.Unhealthy] = StatusCodes.Status503ServiceUnavailable
        }
    });
}
```

### <a name="suppress-cache-headers"></a><span data-ttu-id="87c28-179">캐시 헤더 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="87c28-179">Suppress cache headers</span></span>

<span data-ttu-id="87c28-180">`AllowCachingResponses`는 응답 캐싱을 방지하기 위해 상태 검사 미들웨어가 HTTP 헤더를 프로브 응답에 추가할지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-180">`AllowCachingResponses` controls whether the Health Check Middleware adds HTTP headers to a probe response to prevent response caching.</span></span> <span data-ttu-id="87c28-181">값이 `false`(기본값)인 경우 미들웨어는 응답 캐싱을 방지하기 위해 `Cache-Control`, `Expires` 및 `Pragma` 헤더를 설정하거나 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-181">If the value is `false` (default), the middleware sets or overrides the `Cache-Control`, `Expires`, and `Pragma` headers to prevent response caching.</span></span> <span data-ttu-id="87c28-182">값이 `true`인 경우 미들웨어는 응답 캐시 헤더를 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-182">If the value is `true`, the middleware doesn't modify the cache headers of the response.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // The default value is false.
        AllowCachingResponses = false
    });
}
```

### <a name="customize-output"></a><span data-ttu-id="87c28-183">출력 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="87c28-183">Customize output</span></span>

<span data-ttu-id="87c28-184">`ResponseWriter` 옵션은 응답을 기록하는 데 사용되는 대리자를 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-184">The `ResponseWriter` option gets or sets a delegate used to write the response.</span></span> <span data-ttu-id="87c28-185">기본 대리자는 `HealthReport.Status`의 문자열 값을 사용하여 최소 일반 텍스트 응답을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-185">The default delegate writes a minimal plaintext response with the string value of `HealthReport.Status`.</span></span>

```csharp
using Microsoft.AspNetCore.Diagnostics.HealthChecks;
using Microsoft.Extensions.Diagnostics.HealthChecks;

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseHealthChecks("/health", new HealthCheckOptions()
    {
        // WriteResponse is a delegate used to write the response.
        ResponseWriter = WriteResponse
    });
}

private static Task WriteResponse(HttpContext httpContext, 
    HealthReport result)
{
    httpContext.Response.ContentType = "application/json";

    var json = new JObject(
        new JProperty("status", result.Status.ToString()),
        new JProperty("results", new JObject(result.Entries.Select(pair =>
            new JProperty(pair.Key, new JObject(
                new JProperty("status", pair.Value.Status.ToString()),
                new JProperty("description", pair.Value.Description),
                new JProperty("data", new JObject(pair.Value.Data.Select(
                    p => new JProperty(p.Key, p.Value))))))))));
    return httpContext.Response.WriteAsync(
        json.ToString(Formatting.Indented));
}
```

## <a name="database-probe"></a><span data-ttu-id="87c28-186">데이터베이스 프로브</span><span class="sxs-lookup"><span data-stu-id="87c28-186">Database probe</span></span>

<span data-ttu-id="87c28-187">상태 검사는 데이터베이스 쿼리를 지정하여 데이터베이스가 정상적으로 응답하는지를 나타내기 위해 부울 테스트로서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-187">A health check can specify a database query to run as a boolean test to indicate if the database is responding normally.</span></span>

<span data-ttu-id="87c28-188">샘플 앱은 ASP.NET Core 앱의 상태 검사 라이브러리인 [BeatPulse](https://github.com/Xabaril/BeatPulse)를 사용하여 SQL Server 데이터베이스에 대한 상태 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-188">The sample app uses [BeatPulse](https://github.com/Xabaril/BeatPulse), a health check library for ASP.NET Core apps, to perform a health check on a SQL Server database.</span></span> <span data-ttu-id="87c28-189">BeatPulse는 데이터베이스에 연결이 양호한지 확인하기 위해 데이터베이스에 대해 `SELECT 1` 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-189">BeatPulse executes a `SELECT 1` query against the database to confirm the connection to the database is healthy.</span></span>

> [!WARNING]
> <span data-ttu-id="87c28-190">쿼리로 데이터베이스 연결을 검사할 때 신속하게 반환되는 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-190">When checking a database connection with a query, choose a query that returns quickly.</span></span> <span data-ttu-id="87c28-191">쿼리 방식 실행은 데이터베이스의 오버로드와 성능 저하를 유발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-191">The query approach runs the risk of overloading the database and degrading its performance.</span></span> <span data-ttu-id="87c28-192">대부분의 경우 테스트 쿼리를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-192">In most cases, running a test query isn't necessary.</span></span> <span data-ttu-id="87c28-193">간단히 데이터베이스에 연결하는 정도로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-193">Merely making a successful connection to the database is sufficient.</span></span> <span data-ttu-id="87c28-194">쿼리를 실행해야 하는 경우 `SELECT 1`과 같은 간단한 SELECT 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-194">If you find it necessary to run a query, choose a simple SELECT query, such as `SELECT 1`.</span></span>

<span data-ttu-id="87c28-195">BeatPulse 라이브러리를 사용하려면 [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/)에 대한 패키지 참조를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-195">In order to use the BeatPulse library, include a package reference to [AspNetCore.HealthChecks.SqlServer](https://www.nuget.org/packages/AspNetCore.HealthChecks.SqlServer/).</span></span>

<span data-ttu-id="87c28-196">샘플 앱의 *appsettings.json* 파일에서 유효한 데이터베이스 연결 문자열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-196">Supply a valid database connection string in the *appsettings.json* file of the sample app.</span></span> <span data-ttu-id="87c28-197">앱은 `HealthCheckSample`이라고 하는 SQL Server 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-197">The app uses a SQL Server database named `HealthCheckSample`:</span></span>

[!code-json[](health-checks/samples/2.x/HealthChecksSample/appsettings.json?highlight=3)]

<span data-ttu-id="87c28-198">`Startup.ConfigureServices`의 `AddHealthChecks`에 상태 검사 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-198">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="87c28-199">샘플 앱은 데이터베이스의 연결 문자열(*DbHealthStartup.cs*)을 사용하여 BeatPulse의 `AddSqlServer` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-199">The sample app calls BeatPulse's `AddSqlServer` method with the database's connection string (*DbHealthStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="87c28-200">`Startup.Configure`의 앱 처리 파이프라인에서 상태 검사 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-200">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbHealthStartup.cs?name=snippet_Configure)]

<span data-ttu-id="87c28-201">샘플 앱을 사용하여 데이터베이스 프로브 시나리오를 실행하려면 명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-201">To run the database probe scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario db
```

> [!NOTE]
> <span data-ttu-id="87c28-202">[BeatPulse](https://github.com/Xabaril/BeatPulse)는 Microsoft에서 유지 관리하거나 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-202">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

## <a name="entity-framework-core-dbcontext-probe"></a><span data-ttu-id="87c28-203">Entity Framework Core DbContext 프로브</span><span class="sxs-lookup"><span data-stu-id="87c28-203">Entity Framework Core DbContext probe</span></span>

<span data-ttu-id="87c28-204">`DbContext` 검사는 [EF(Entity Framework) Core](/ef/core/)를 사용하는 앱에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-204">The `DbContext` check is supported in apps that use [Entity Framework (EF) Core](/ef/core/).</span></span> <span data-ttu-id="87c28-205">이 검사는 앱이 EF Core `DbContext`에 대해 구성된 데이터베이스와 통신할 수 있음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-205">This check confirms that the app can communicate with the database configured for an EF Core `DbContext`.</span></span> <span data-ttu-id="87c28-206">기본적으로 `DbContextHealthCheck`는 EF Core의 `CanConnectAsync` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-206">By default, the `DbContextHealthCheck` calls EF Core's `CanConnectAsync` method.</span></span> <span data-ttu-id="87c28-207">`AddDbContextCheck` 메서드의 오버로드를 사용하여 상태를 검사할 때 실행되는 작업을 사용자 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-207">You can customize what operation is run when checking health using overloads of the `AddDbContextCheck` method.</span></span>

<span data-ttu-id="87c28-208">`AddDbContextCheck<TContext>`는 `DbContext`(`TContext`)에 대한 상태 검사를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-208">`AddDbContextCheck<TContext>` registers a health check for a `DbContext` (`TContext`).</span></span> <span data-ttu-id="87c28-209">기본적으로 상태 검사의 이름은 `TContext` 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-209">By default, the name of the health check is the name of the `TContext` type.</span></span> <span data-ttu-id="87c28-210">오버로드는 오류 상태, 태그 및 사용자 지정 테스트 쿼리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-210">An overload is available to configure the failure status, tags, and a custom test query.</span></span>

<span data-ttu-id="87c28-211">샘플 앱에서 `AppDbContext`는 `AddDbContextCheck`에 제공되고 `Startup.ConfigureServices`의 서비스로서 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-211">In the sample app, `AppDbContext` is provided to `AddDbContextCheck` and registered as a service in `Startup.ConfigureServices`.</span></span>

<span data-ttu-id="87c28-212">*DbContextHealthStartup.cs*:</span><span class="sxs-lookup"><span data-stu-id="87c28-212">*DbContextHealthStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="87c28-213">샘플 앱에서 `UseHealthChecks`는 `Startup.Configure`에서 상태 검사 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-213">In the sample app, `UseHealthChecks` adds the Health Check Middleware in `Startup.Configure`.</span></span>

<span data-ttu-id="87c28-214">*DbContextHealthStartup.cs*:</span><span class="sxs-lookup"><span data-stu-id="87c28-214">*DbContextHealthStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/DbContextHealthStartup.cs?name=snippet_Configure)]

<span data-ttu-id="87c28-215">샘플 앱을 사용하여 `DbContext` 프로브 시나리오를 실행하려면 연결 문자열에 의해 지정된 데이터베이스가 SQL Server 인스턴스에 존재하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-215">To run the `DbContext` probe scenario using the sample app, confirm that the database specified by the the connection string doesn't exist in the SQL Server instance.</span></span> <span data-ttu-id="87c28-216">데이터베이스가 있으면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-216">If the database exists, delete it.</span></span>

<span data-ttu-id="87c28-217">명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-217">Execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario dbcontext
```

<span data-ttu-id="87c28-218">앱을 실행한 후 브라우저의 `/health` 엔드포인트에 요청하여 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-218">After the app is running, check the health status by making a request to the `/health` endpoint in a browser.</span></span> <span data-ttu-id="87c28-219">데이터베이스 및 `AppDbContext`가 존재하기 않기 때문에 앱은 다음 응답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-219">The database and `AppDbContext` don't exist, so app provides the following response:</span></span>

```
Unhealthy
```

<span data-ttu-id="87c28-220">데이터베이스를 만드는 샘플 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-220">Trigger the sample app to create the database.</span></span> <span data-ttu-id="87c28-221">`/createdatabase`에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-221">Make a request to `/createdatabase`.</span></span> <span data-ttu-id="87c28-222">앱은 다음과 같이 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-222">The app responds:</span></span>

```
Creating the database...
Done!
Navigate to /health to see the health status.
```

<span data-ttu-id="87c28-223">`/health` 엔드포인트에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-223">Make a request to the `/health` endpoint.</span></span> <span data-ttu-id="87c28-224">데이터베이스와 컨텍스트가 존재하기 때문에 앱은 다음과 같이 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-224">The database and context exist, so app responds:</span></span>

```
Healthy
```

<span data-ttu-id="87c28-225">데이터베이스를 삭제하는 샘플 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-225">Trigger the sample app to delete the database.</span></span> <span data-ttu-id="87c28-226">`/deletedatabase`에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-226">Make a request to `/deletedatabase`.</span></span> <span data-ttu-id="87c28-227">앱은 다음과 같이 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-227">The app responds:</span></span>

```
Deleting the database...
Done!
Navigate to /health to see the health status.
```

<span data-ttu-id="87c28-228">`/health` 엔드포인트에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-228">Make a request to the `/health` endpoint.</span></span> <span data-ttu-id="87c28-229">앱은 다음과 같이 비정상 응답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-229">The app provides an unhealthy response:</span></span>

```
Unhealthy
```

## <a name="separate-readiness-and-liveness-probes"></a><span data-ttu-id="87c28-230">별도의 준비 상태 및 활동성 프로브</span><span class="sxs-lookup"><span data-stu-id="87c28-230">Separate readiness and liveness probes</span></span>

<span data-ttu-id="87c28-231">일부 호스팅 시나리오에서 두 개의 앱 상태를 구분하는 한 쌍의 상태 검사가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-231">In some hosting scenarios, a pair of health checks are used that distinguish two app states:</span></span>

* <span data-ttu-id="87c28-232">앱은 작동하지만, 아직 요청을 받을 준비가 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-232">The app is functioning but not yet ready to receive requests.</span></span> <span data-ttu-id="87c28-233">이 상태는 앱의 *준비 상태*입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-233">This state is the app's *readiness*.</span></span>
* <span data-ttu-id="87c28-234">앱을 작동하고 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-234">The app is functioning and responding to requests.</span></span> <span data-ttu-id="87c28-235">이 상태는 앱의 *활동성*입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-235">This state is the app's *liveness*.</span></span>

<span data-ttu-id="87c28-236">준비 상태 검사는 대개 앱의 하위 시스템 및 리소스를 모두 사용할 수 있는지 확인하기 위해 보다 광범위하고 시간이 많이 소요되는 검사 세트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-236">The readiness check usually performs a more extensive and time-consuming set of checks to determine if all of the app's subsystems and resources are available.</span></span> <span data-ttu-id="87c28-237">활동성 검사는 앱이 요청을 처리할 수 있는지 여부를 확인하기 위해 빠른 검사만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-237">A liveness check merely performs a quick check to determine if the app is available to process requests.</span></span> <span data-ttu-id="87c28-238">앱이 준비 상태 검사를 통과한 후에는 값 비싼 준비 상태 검사 세트로 앱에 추가로 부담 지울 필요가 없으며&mdash;이후 활동성에 대한 검사만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-238">After the app passes its readiness check, there's no need to burden the app further with the expensive set of readiness checks&mdash;further checks only require checking for liveness.</span></span>

<span data-ttu-id="87c28-239">샘플 앱에는 [호스팅된 서비스](xref:fundamentals/host/hosted-services)에서 장기 실행 시작 작업 완료를 보고하는 상태 검사가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-239">The sample app contains a health check to report the completion of long-running startup task in a [Hosted Service](xref:fundamentals/host/hosted-services).</span></span> <span data-ttu-id="87c28-240">`StartupHostedServiceHealthCheck`는 장기 실행 작업이 완료되면(*StartupHostedServiceHealthCheck.cs*) 호스팅된 서비스를 `true`로 설정할 수 있는 속성 `StartupTaskCompleted`를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-240">The `StartupHostedServiceHealthCheck` exposes a property, `StartupTaskCompleted`, that the hosted service can set to `true` when its long-running task is finished (*StartupHostedServiceHealthCheck.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/StartupHostedServiceHealthCheck.cs?name=snippet1&highlight=5)]

<span data-ttu-id="87c28-241">장기 실행 백그라운드 작업은 [호스팅된 서비스](xref:fundamentals/host/hosted-services)(*Services/StartupHostedService*)에 의해 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-241">The long-running background task is started by a [Hosted Service](xref:fundamentals/host/hosted-services) (*Services/StartupHostedService*).</span></span> <span data-ttu-id="87c28-242">작업이 끝나면 `StartupHostedServiceHealthCheck.StartupTaskCompleted`는 `true`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-242">At the conclusion of the task, `StartupHostedServiceHealthCheck.StartupTaskCompleted` is set to `true`:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/Services/StartupHostedService.cs?name=snippet1&highlight=18-20)]

<span data-ttu-id="87c28-243">상태 검사는 호스팅된 서비스와 함께 `Startup.ConfigureServices`의 `AddCheck`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-243">The health check is registered with `AddCheck` in `Startup.ConfigureServices` along with the hosted service.</span></span> <span data-ttu-id="87c28-244">호스팅된 서비스가 상태 검사에서 속성을 설정해야 하기 때문에 상태 확인도 서비스 컨테이너(*LivenessProbeStartup.cs*)에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-244">Because the hosted service must set the property on the health check, the health check is also registered in the service container (*LivenessProbeStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_ConfigureServices)]

<span data-ttu-id="87c28-245">`Startup.Configure`의 앱 처리 파이프라인에서 상태 검사 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-245">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`.</span></span> <span data-ttu-id="87c28-246">샘플 앱에서 상태 검사 엔드포인트는 활동성 검사의 경우 `/health/ready`에, 준비 상태 검사의 경우 `/health/live`에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-246">In the sample app, the health check endpoints are created at `/health/ready` for the readiness check and `/health/live` for the liveness check.</span></span> <span data-ttu-id="87c28-247">준비 상태 검사는 `ready` 태그가 있는 상태 검사에서 상태 검사를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-247">The readiness check filters health checks to the health check with the `ready` tag.</span></span> <span data-ttu-id="87c28-248">활동성 검사는 `HealthCheckOptions.Predicate`에서 `false`를 반환하여 `StartupHostedServiceHealthCheck`를 필터링합니다(자세한 내용은 [상태 검사 필터링](#filter-health-checks) 참조).</span><span class="sxs-lookup"><span data-stu-id="87c28-248">The liveness check filters out the `StartupHostedServiceHealthCheck` by returning `false` in the `HealthCheckOptions.Predicate` (for more information, see [Filter health checks](#filter-health-checks)):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/LivenessProbeStartup.cs?name=snippet_Configure)]

<span data-ttu-id="87c28-249">샘플 앱을 사용하여 준비 상태/활동성 구성 시나리오를 실행하려면 명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-249">To run the readiness/liveness configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario liveness
```

<span data-ttu-id="87c28-250">브라우저에서 15초가 경과할 때까지 `/health/ready`를 여러 번 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-250">In a browser, visit `/health/ready` several times until 15 seconds have passed.</span></span> <span data-ttu-id="87c28-251">상태 검사는 첫 15초 동안 `Unhealthy`를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-251">The health check reports `Unhealthy` for the first 15 seconds.</span></span> <span data-ttu-id="87c28-252">15초 후, 엔드포인트는 `Healthy`를 보고하여 호스팅된 서비스에 의해 장기 실행 작업이 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-252">After 15 seconds, the endpoint reports `Healthy`, which reflects the completion of the long-running task by the hosted service.</span></span>

### <a name="kubernetes-example"></a><span data-ttu-id="87c28-253">Kubernetes 예제</span><span class="sxs-lookup"><span data-stu-id="87c28-253">Kubernetes example</span></span>

<span data-ttu-id="87c28-254">별도의 준비 상태 및 활동성 검사를 사용하는 것은 [Kubernetes](https://kubernetes.io/)와 같은 환경에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-254">Using separate readiness and liveness checks is useful in an environment such as [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="87c28-255">Kubernetes에서 앱은 기본 데이터베이스 가용성 테스트와 같이 요청을 수락하기 전에 시간이 많이 걸리는 시작 작업을 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-255">In Kubernetes, an app might be required to perform time-consuming startup work before accepting requests, such as a test of the underlying database availability.</span></span> <span data-ttu-id="87c28-256">별도의 검사를 사용하면 오케스트레이터가 앱이 작동하고 있지만 아직 준비가 되지 않았는지 또는 앱이 시작되지 않았는지 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-256">Using separate checks allows the orchestrator to distinguish whether the app is functioning but not yet ready or if the app has failed to start.</span></span> <span data-ttu-id="87c28-257">Kubernetes의 준비 상태 및 활동성 프로브에 대한 자세한 내용은 Kubernetes 설명서의 [활동성 및 준비 상태 프로브 구성](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87c28-257">For more information on readiness and liveness probes in Kubernetes, see [Configure Liveness and Readiness Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) in the Kubernetes documentation.</span></span>

<span data-ttu-id="87c28-258">다음 예제는 Kubernetes 준비 상태 프로브 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-258">The following example demonstrates a Kubernetes readiness probe configuration:</span></span>

```
spec:
  template:
  spec:
    readinessProbe:
      # an http probe
      httpGet:
        path: /health/ready
        port: 80
      # length of time to wait for a pod to initialize
      # after pod startup, before applying health checking
      initialDelaySeconds: 30
      timeoutSeconds: 1
    ports:
      - containerPort: 80
```

## <a name="metric-based-probe-with-a-custom-response-writer"></a><span data-ttu-id="87c28-259">사용자 지정 응답 기록기가 있는 메트릭 기반 프로브</span><span class="sxs-lookup"><span data-stu-id="87c28-259">Metric-based probe with a custom response writer</span></span>

<span data-ttu-id="87c28-260">샘플 앱은 사용자 지정 응답 기록기가 있는 메모리 상태를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-260">The sample app demonstrates a memory health check with a custom response writer.</span></span>

<span data-ttu-id="87c28-261">앱이 일정한 메모리 임계값(샘플 앱의 경우 1GB)을 초과하여 사용하는 경우 `MemoryHealthCheck`는 성능이 저하된 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-261">`MemoryHealthCheck` reports a degraded status if the app uses more than a given threshold of memory (1 GB in the sample app).</span></span> <span data-ttu-id="87c28-262">`HealthCheckResult`에는 앱의 가비지 수집기(GC) 정보가 포함됩니다(*MemoryHealthCheck.cs*).</span><span class="sxs-lookup"><span data-stu-id="87c28-262">The `HealthCheckResult` includes Garbage Collector (GC) information for the app (*MemoryHealthCheck.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/MemoryHealthCheck.cs?name=snippet1)]

<span data-ttu-id="87c28-263">`Startup.ConfigureServices`의 `AddHealthChecks`에 상태 검사 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-263">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="87c28-264">`AddCheck`에 전달하여 상태 검사를 사용하는 대신 `MemoryHealthCheck`는 서비스로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-264">Instead of enabling the health check by passing it to `AddCheck`, the `MemoryHealthCheck` is registered as a service.</span></span> <span data-ttu-id="87c28-265">모든 `IHealthCheck` 등록된 서비스는 상태 검사 서비스 및 미들웨어에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-265">All `IHealthCheck` registered services are available to the health check services and middleware.</span></span> <span data-ttu-id="87c28-266">상태 확인 서비스를 Singleton 서비스로 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-266">We recommend registering health check services as Singleton services.</span></span>

<span data-ttu-id="87c28-267">*CustomWriterStartup.cs*:</span><span class="sxs-lookup"><span data-stu-id="87c28-267">*CustomWriterStartup.cs*:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_ConfigureServices&highlight=4)]

<span data-ttu-id="87c28-268">`Startup.Configure`의 앱 처리 파이프라인에서 상태 검사 미들웨어를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-268">Call Health Check Middleware in the app processing pipeline in `Startup.Configure`.</span></span> <span data-ttu-id="87c28-269">상태 검사가 실행될 때 사용자 정의 JSON 응답을 출력하기 위해 `ResponseWriter` 속성에 `WriteResponse` 대리자가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-269">A `WriteResponse` delegate is provided to the `ResponseWriter` property to output a custom JSON response when the health check executes:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_Configure&highlight=6)]

<span data-ttu-id="87c28-270">`WriteResponse` 메서드는 `CompositeHealthCheckResult`를 JSON 객체로 형식 지정하고 상태 검사 응답을 위해 JSON 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-270">The `WriteResponse` method formats the `CompositeHealthCheckResult` into a JSON object and yields JSON output for the health check response:</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/CustomWriterStartup.cs?name=snippet_WriteResponse)]

<span data-ttu-id="87c28-271">샘플 앱을 사용하여 사용자 지정 응답 기록기 출력으로 메트릭 기반 프로브를 실행하려면 명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-271">To run the metric-based probe with custom response writer output using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario writer
```

> [!NOTE]
> <span data-ttu-id="87c28-272">[BeatPulse](https://github.com/Xabaril/BeatPulse)에는 디스크 스토리지 및 최댓값 활동성 검사를 포함하여 메트릭 기반 상태 확인 시나리오가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-272">[BeatPulse](https://github.com/Xabaril/BeatPulse) includes metric-based health check scenarios, including disk storage and maximum value liveness checks.</span></span>
>
> <span data-ttu-id="87c28-273">[BeatPulse](https://github.com/Xabaril/BeatPulse)는 Microsoft에서 유지 관리하거나 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-273">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>

## <a name="filter-by-port"></a><span data-ttu-id="87c28-274">포트별 필터링</span><span class="sxs-lookup"><span data-stu-id="87c28-274">Filter by port</span></span>

<span data-ttu-id="87c28-275">포트와 함께 `UseHealthChecks`를 호출하면 지정된 포트에 대한 상태 검사 요청을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-275">Calling `UseHealthChecks` with a port restricts health check requests to the port specified.</span></span> <span data-ttu-id="87c28-276">이는 일반적으로 컨테이너 환경에서 서비스 모니터링을 위해 포트를 노출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-276">This is typically used in a container environment to expose a port for monitoring services.</span></span>

<span data-ttu-id="87c28-277">샘플 앱은 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 사용하여 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-277">The sample app configures the port using the [Environment Variable Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span> <span data-ttu-id="87c28-278">포트는 *launchSettings.json* 파일에서 설정되고 환경 변수를 통해 구성 공급자에게 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-278">The port is set in the *launchSettings.json* file and passed to the configuration provider via an environment variable.</span></span> <span data-ttu-id="87c28-279">또한 관리 포트에서 요청을 수신하도록 서버를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-279">You must also configure the server to listen to requests on the management port.</span></span>

<span data-ttu-id="87c28-280">샘플 앱을 사용하여 관리 포트 구성을 보여주려면 *launchSettings.json* 파일을 *Properties* 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-280">To use the sample app to demonstrate management port configuration, create the *launchSettings.json* file in a *Properties* folder.</span></span>

<span data-ttu-id="87c28-281">다음 *launchSettings.json* 파일은 샘플 앱의 프로젝트 파일에 포함되지 않으며 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-281">The following *launchSettings.json* file isn't included in the sample app's project files and must be created manually.</span></span>

<span data-ttu-id="87c28-282">*Properties/launchSettings.json*:</span><span class="sxs-lookup"><span data-stu-id="87c28-282">*Properties/launchSettings.json*:</span></span>

```json
{
  "profiles": {
    "SampleApp": {
      "commandName": "Project",
      "commandLineArgs": "",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "ASPNETCORE_URLS": "http://localhost:5000/;http://localhost:5001/",
        "ASPNETCORE_MANAGEMENTPORT": "5001"
      },
      "applicationUrl": "http://localhost:5000/"
    }
  }
}
```

<span data-ttu-id="87c28-283">`Startup.ConfigureServices`의 `AddHealthChecks`에 상태 검사 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-283">Register health check services with `AddHealthChecks` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="87c28-284">`UseHealthChecks`에 대한 호출은 관리 포트를 지정합니다(*ManagementPortStartup.cs*).</span><span class="sxs-lookup"><span data-stu-id="87c28-284">The call to `UseHealthChecks` specifies the management port (*ManagementPortStartup.cs*):</span></span>

[!code-csharp[](health-checks/samples/2.x/HealthChecksSample/ManagementPortStartup.cs?name=snippet1&highlight=12,18)]

> [!NOTE]
> <span data-ttu-id="87c28-285">코드에서 URL과 관리 포트를 명시적으로 설정하여 샘플 앱에 *launchSettings.json* 파일을 만들지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-285">You can avoid creating the *launchSettings.json* file in the sample app by setting the URLs and management port explicitly in code.</span></span> <span data-ttu-id="87c28-286">`WebHostBuilder`가 만들어진 *Program.cs*에서 `UseUrls`에 호출을 추가하고 앱의 정상적인 응답 엔드포인트와 관리 포트 엔드포인트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-286">In *Program.cs* where the `WebHostBuilder` is created, add a call to `UseUrls` and provide the app's normal response endpoint and the management port endpoint.</span></span> <span data-ttu-id="87c28-287">`UseHealthChecks`가 호출되는 *ManagementPortStartup.cs*에서 관리 포트를 명시적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-287">In *ManagementPortStartup.cs* where `UseHealthChecks` is called, specify the management port explicitly.</span></span>
>
> <span data-ttu-id="87c28-288">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="87c28-288">*Program.cs*:</span></span>
>
> ```csharp
> return new WebHostBuilder()
>     .UseConfiguration(config)
>     .UseUrls("http://localhost:5000/;http://localhost:5001/")
>     .ConfigureLogging(builder =>
>     {
>         builder.SetMinimumLevel(LogLevel.Trace);
>         builder.AddConfiguration(config);
>         builder.AddConsole();
>     })
>     .UseKestrel()
>     .UseStartup(startupType)
>     .Build();
> ```
>
> <span data-ttu-id="87c28-289">*ManagementPortStartup.cs*:</span><span class="sxs-lookup"><span data-stu-id="87c28-289">*ManagementPortStartup.cs*:</span></span>
>
> ```csharp
> app.UseHealthChecks("/health", port: 5001);
> ```

<span data-ttu-id="87c28-290">샘플 앱을 사용하여 관리 포트 구성 시나리오를 실행하려면 명령 셸의 프로젝트 폴더에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-290">To run the management port configuration scenario using the sample app, execute the following command from the project's folder in a command shell:</span></span>

```console
dotnet run --scenario port
```

## <a name="distribute-a-health-check-library"></a><span data-ttu-id="87c28-291">상태 검사 라이브러리 배포</span><span class="sxs-lookup"><span data-stu-id="87c28-291">Distribute a health check library</span></span>

<span data-ttu-id="87c28-292">상태 검사를 라이브러리로 배포하려면 다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-292">To distribute a health check as a library:</span></span>

1. <span data-ttu-id="87c28-293">`IHealthCheck` 인터페이스를 독립 실행형 클래스로 구현하는 상태 검사를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-293">Write a health check that implements the `IHealthCheck` interface as a standalone class.</span></span> <span data-ttu-id="87c28-294">클래스는 [DI(종속성 주입)](xref:fundamentals/dependency-injection), 유형 활성화 및 [명명된 옵션](xref:fundamentals/configuration/options)에 의존하여 구성 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-294">The class can rely on [dependency injection (DI)](xref:fundamentals/dependency-injection), type activation, and [named options](xref:fundamentals/configuration/options) to access configuration data.</span></span>

   ```csharp
   using System;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   namespace SampleApp
   {
       public class ExampleHealthCheck : IHealthCheck
       {
           private readonly string _data1;
           private readonly int? _data2;

           public ExampleHealthCheck(string data1, int? data2)
           {
               _data1 = data1 ?? throw new ArgumentNullException(nameof(data1));
               _data2 = data2 ?? throw new ArgumentNullException(nameof(data2));
           }

           public async Task<HealthCheckResult> CheckHealthAsync(
               HealthCheckContext context, CancellationToken cancellationToken)
           {
               try
               {
                   // Health check logic
                   //
                   // data1 and data2 are used in the method to
                   // run the probe's health check logic.

                   // Assume that it's possible for this health check
                   // to throw an AccessViolationException.

                   return HealthCheckResult.Healthy();
               }
               catch (AccessViolationException ex)
               {
                   return new HealthCheckResult(
                       context.Registration.FailureStatus,
                       description: "An access violation occurred during the check.",
                       exception: ex,
                       data: null);
               }
           }
       }
   }
   ```

1. <span data-ttu-id="87c28-295">사용하는 앱이 `Startup.Configure` 메서드에서 호출하는 매개 변수를 사용하여 확장 메서드를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-295">Write an extension method with parameters that the consuming app calls in its `Startup.Configure` method.</span></span> <span data-ttu-id="87c28-296">다음 예제에서는 다음 상태 검사 메서드 서명을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-296">In the following example, assume the following health check method signature:</span></span>

   ```csharp
   ExampleHealthCheck(string, string, int )
   ```

   <span data-ttu-id="87c28-297">이전 서명은 `ExampleHealthCheck`가 상태 검사 프로브 로직을 처리하기 위해 추가 데이터가 필요함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-297">The preceding signature indicates that the `ExampleHealthCheck` requires additional data to process the health check probe logic.</span></span> <span data-ttu-id="87c28-298">상태 검사가 확장 메서드를 사용하여 등록되면 데이터는 상태 검사 인스턴스를 만드는 데 사용된 대리자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-298">The data is provided to the delegate used to create the health check instance when the health check is registered with an extension method.</span></span> <span data-ttu-id="87c28-299">다음 예제에서 호출자는 선택 사항을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-299">In the following example, the caller specifies optional:</span></span>

   * <span data-ttu-id="87c28-300">상태 검사 이름(`name`).</span><span class="sxs-lookup"><span data-stu-id="87c28-300">health check name (`name`).</span></span> <span data-ttu-id="87c28-301">`null`인 경우 `example_health_check`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-301">If `null`, `example_health_check` is used.</span></span>
   * <span data-ttu-id="87c28-302">상태 검사를 위한 문자열 데이터 요소입니다(`data1`).</span><span class="sxs-lookup"><span data-stu-id="87c28-302">string data point for the health check (`data1`).</span></span>
   * <span data-ttu-id="87c28-303">상태 검사를 위한 정수 데이터 요소입니다(`data2`).</span><span class="sxs-lookup"><span data-stu-id="87c28-303">integer data point for the health check (`data2`).</span></span> <span data-ttu-id="87c28-304">`null`인 경우 `1`이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-304">If `null`, `1` is used.</span></span>
   * <span data-ttu-id="87c28-305">실패 상태입니다(`HealthStatus`).</span><span class="sxs-lookup"><span data-stu-id="87c28-305">failure status (`HealthStatus`).</span></span> <span data-ttu-id="87c28-306">기본값은 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-306">The default is `null`.</span></span> <span data-ttu-id="87c28-307">`null`인 경우 `HealthStatus.Unhealthy`는 오류 상태에 대해 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-307">If `null`, `HealthStatus.Unhealthy` is reported for a failure status.</span></span>
   * <span data-ttu-id="87c28-308">태그(`IEnumerable<string>`)입니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-308">tags (`IEnumerable<string>`).</span></span>

   ```csharp
   using System.Collections.Generic;
   using Microsoft.Extensions.Diagnostics.HealthChecks;

   public static class ExampleHealthCheckBuilderExtensions
   {
       const string NAME = "example_health_check";

       public static IHealthChecksBuilder AddExampleHealthCheck(
           this IHealthChecksBuilder builder, 
           string name = default, 
           string data1, 
           int data2 = 1, 
           HealthStatus? failureStatus = default, 
           IEnumerable<string> tags = default)
       {
           return builder.Add(new HealthCheckRegistration(
               name ?? NAME,
               sp => new ExampleHealthCheck(data1, data2),
               failureStatus,
               tags));
       }
   }
   ```

## <a name="health-check-publisher"></a><span data-ttu-id="87c28-309">상태 검사 게시자</span><span class="sxs-lookup"><span data-stu-id="87c28-309">Health Check Publisher</span></span>

<span data-ttu-id="87c28-310">`IHealthCheckPublisher`가 서비스 컨테이너에 추가되면 상태 검사 시스템이 주기적으로 상태 검사를 실행하고 그 결과로 `PublishAsync`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-310">When an `IHealthCheckPublisher` is added to the service container, the health check system periodically executes your health checks and calls `PublishAsync` with the result.</span></span> <span data-ttu-id="87c28-311">이는 각 프로세스가 상태를 결정하기 위해 주기적으로 모니터링 시스템을 호출하도록 하는 푸시 기반 상태 모니터링 시스템 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-311">This is useful in a push-based health monitoring system scenario that expects each process to call the monitoring system periodically in order to determine health.</span></span>

<span data-ttu-id="87c28-312">`IHealthCheckPublisher` 인터페이스는 단일 메서드를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-312">The `IHealthCheckPublisher` interface has a single method:</span></span>

```csharp
Task PublishAsync(HealthReport report, CancellationToken cancellationToken);
```

> [!NOTE]
> <span data-ttu-id="87c28-313">[BeatPulse](https://github.com/Xabaril/BeatPulse)는 [Application Insights](/azure/application-insights/app-insights-overview)를 포함하여 몇몇 시스템에 대한 게시자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-313">[BeatPulse](https://github.com/Xabaril/BeatPulse) includes publishers for several systems, including [Application Insights](/azure/application-insights/app-insights-overview).</span></span>
>
> <span data-ttu-id="87c28-314">[BeatPulse](https://github.com/Xabaril/BeatPulse)는 Microsoft에서 유지 관리하거나 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c28-314">[BeatPulse](https://github.com/Xabaril/BeatPulse) isn't maintained or supported by Microsoft.</span></span>