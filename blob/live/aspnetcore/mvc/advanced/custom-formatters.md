---
title: "ASP.NET Core MVC 웹 Api에에서 대 한 사용자 지정 포맷터"
author: tdykstra
description: "만들고 ASP.NET Core의 웹 Api에 대 한 사용자 지정 포맷터를 사용 하는 방법을 알아봅니다."
ms.author: tdykstra
manager: wpickett
ms.date: 02/08/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/models/custom-formatters
ms.openlocfilehash: 3a6474fdae29b170978226de74d523b20a16cd0c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="custom-formatters-in-aspnet-core-mvc-web-apis"></a><span data-ttu-id="031c2-103">ASP.NET Core MVC 웹 Api에에서 대 한 사용자 지정 포맷터</span><span class="sxs-lookup"><span data-stu-id="031c2-103">Custom formatters in ASP.NET Core MVC web APIs</span></span>

<span data-ttu-id="031c2-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="031c2-104">By [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="031c2-105">ASP.NET Core MVC JSON, XML 또는 일반 텍스트 형식을 사용 하 여 web Api의에서 데이터 교환에 대 한 기본 제공 지원을에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-105">ASP.NET Core MVC has built-in support for data exchange in web APIs by using JSON, XML, or plain text formats.</span></span> <span data-ttu-id="031c2-106">이 문서에서는 사용자 지정 포맷터를 만들어 추가 형식에 대 한 지원을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-106">This article shows how to add support for additional formats by creating custom formatters.</span></span>

<span data-ttu-id="031c2-107">[보기 또는 GitHub에서 샘플을 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-107">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample).</span></span>

## <a name="when-to-use-custom-formatters"></a><span data-ttu-id="031c2-108">사용자 지정 포맷터를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="031c2-108">When to use custom formatters</span></span>

<span data-ttu-id="031c2-109">하려는 경우에 사용자 지정 포맷터를 사용 하 여는 [콘텐츠 협상](xref:mvc/models/formatting) 기본 제공 포맷터 (JSON, XML 및 일반 텍스트)에서 지원 되지 않는 콘텐츠 형식을 지원 하기 위해 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-109">Use a custom formatter when you want the [content negotiation](xref:mvc/models/formatting) process to support a content type that isn't supported by the built-in formatters (JSON, XML, and plain text).</span></span>

<span data-ttu-id="031c2-110">예를 들어, 웹 API에 대 한 클라이언트 중 일부를 처리할 수 있으면는 [Protobuf](https://github.com/google/protobuf) 형식으로 하려는 경우도 더 효율적 이므로 클라이언트 Protobuf를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-110">For example, if some of the clients for your web API can handle the [Protobuf](https://github.com/google/protobuf) format, you might want to use Protobuf with those clients because it's more efficient.</span></span>  <span data-ttu-id="031c2-111">Web API 연락처 이름 및 주소를 보내도록 할 수 있습니다 또는 [vCard](https://wikipedia.org/wiki/VCard) 형식, 연락 데이터를 교환 하는 데 자주 사용 되는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-111">Or you might want your web API to send contact names and addresses in [vCard](https://wikipedia.org/wiki/VCard) format, a commonly used format for exchanging contact data.</span></span> <span data-ttu-id="031c2-112">이 문서와 함께 제공 되는 샘플 응용 프로그램 간단한 vCard 포맷터를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-112">The sample app provided with this article implements a simple vCard formatter.</span></span>

## <a name="overview-of-how-to-use-a-custom-formatter"></a><span data-ttu-id="031c2-113">사용자 지정 포맷터를 사용 하는 방법의 개요</span><span class="sxs-lookup"><span data-stu-id="031c2-113">Overview of how to use a custom formatter</span></span>

<span data-ttu-id="031c2-114">만들고 사용자 지정 포맷터를 사용 하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-114">Here are the steps to create and use a custom formatter:</span></span>

* <span data-ttu-id="031c2-115">클라이언트에 보낼 데이터를 serialize 하려는 경우에 출력 포맷터 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-115">Create an output formatter class if you want to serialize data to send to the client.</span></span>
* <span data-ttu-id="031c2-116">클라이언트에서 받은 데이터를 deserialize 하려는 경우에 입력된 포맷터 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-116">Create an input formatter class if you want to deserialize data received from the client.</span></span> 
* <span data-ttu-id="031c2-117">추가 하 여 포맷터의 인스턴스는 `InputFormatters` 및 `OutputFormatters` 에서 컬렉션 [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-117">Add instances of your formatters to the `InputFormatters` and `OutputFormatters` collections in [MvcOptions](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.mvcoptions).</span></span>

<span data-ttu-id="031c2-118">다음 섹션에서는 이러한 각 단계에 대 한 지침 및 코드 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-118">The following sections provide guidance and code examples for each of these steps.</span></span>

## <a name="how-to-create-a-custom-formatter-class"></a><span data-ttu-id="031c2-119">사용자 지정 포맷터 클래스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="031c2-119">How to create a custom formatter class</span></span>

<span data-ttu-id="031c2-120">포맷터를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="031c2-120">To create a formatter:</span></span>

* <span data-ttu-id="031c2-121">해당 기본 클래스에서 클래스를 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-121">Derive the class from the appropriate base class.</span></span>
* <span data-ttu-id="031c2-122">생성자에 유효한 미디어 형식 및 인코딩에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-122">Specify valid media types and encodings in the constructor.</span></span>
* <span data-ttu-id="031c2-123">재정의 `CanReadType` / `CanWriteType` 메서드</span><span class="sxs-lookup"><span data-stu-id="031c2-123">Override `CanReadType`/`CanWriteType` methods</span></span>
* <span data-ttu-id="031c2-124">재정의 `ReadRequestBodyAsync` / `WriteResponseBodyAsync` 메서드</span><span class="sxs-lookup"><span data-stu-id="031c2-124">Override `ReadRequestBodyAsync`/`WriteResponseBodyAsync` methods</span></span>
  
### <a name="derive-from-the-appropriate-base-class"></a><span data-ttu-id="031c2-125">적절 한 기본 클래스에서 파생</span><span class="sxs-lookup"><span data-stu-id="031c2-125">Derive from the appropriate base class</span></span>

<span data-ttu-id="031c2-126">텍스트 미디어 유형 (예를 들어 vCard)에 대 한 파생은 [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) 또는 [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-126">For text media types (for example, vCard), derive from the [TextInputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) or [TextOutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) base class.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

<span data-ttu-id="031c2-127">이진 형식의 파생 된 [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) 또는 [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-127">For binary types, derive from the [InputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.inputformatter) or [OutputFormatter](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformatter) base class.</span></span>

### <a name="specify-valid-media-types-and-encodings"></a><span data-ttu-id="031c2-128">유효한 미디어 형식 및 인코딩에서 지정</span><span class="sxs-lookup"><span data-stu-id="031c2-128">Specify valid media types and encodings</span></span>

<span data-ttu-id="031c2-129">생성자에 유효한 미디어 형식 및 인코딩에서 추가 하 여 지정 하는 `SupportedMediaTypes` 및 `SupportedEncodings` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-129">In the constructor, specify valid media types and encodings by adding to the `SupportedMediaTypes` and `SupportedEncodings` collections.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

> [!NOTE]  
> <span data-ttu-id="031c2-130">포맷터 클래스의 생성자 종속성 주입을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-130">You can't do constructor dependency injection in a formatter class.</span></span> <span data-ttu-id="031c2-131">예를 들어 생성자에로 거 매개 변수를 추가 하 여로 거를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-131">For example, you can't get a logger by adding a logger parameter to the constructor.</span></span> <span data-ttu-id="031c2-132">서비스에 액세스 하려면 메서드에 전달 된 컨텍스트 개체를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-132">To access services, you have to use the context object that gets passed in to your methods.</span></span> <span data-ttu-id="031c2-133">코드 예제를 보려면 [아래](#read-write) 이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-133">A code example [below](#read-write) shows how to do this.</span></span>

### <a name="override-canreadtypecanwritetype"></a><span data-ttu-id="031c2-134">Override CanReadType/CanWriteType</span><span class="sxs-lookup"><span data-stu-id="031c2-134">Override CanReadType/CanWriteType</span></span> 

<span data-ttu-id="031c2-135">Á ´ â 재정의 하 여에서 serialize 하거나 deserialize 수는 `CanReadType` 또는 `CanWriteType` 메서드.</span><span class="sxs-lookup"><span data-stu-id="031c2-135">Specify the type you can deserialize into or serialize from by overriding the `CanReadType` or `CanWriteType` methods.</span></span> <span data-ttu-id="031c2-136">VCard 텍스트에서 만들 수만 예를 들어 한 `Contact` 형식 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-136">For example, you might only be able to create vCard text from a `Contact` type and vice versa.</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

#### <a name="the-canwriteresult-method"></a><span data-ttu-id="031c2-137">CanWriteResult 메서드</span><span class="sxs-lookup"><span data-stu-id="031c2-137">The CanWriteResult method</span></span>

<span data-ttu-id="031c2-138">일부 시나리오에서 무시 해야 `CanWriteResult` 대신 `CanWriteType`합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-138">In some scenarios you have to override `CanWriteResult` instead of `CanWriteType`.</span></span> <span data-ttu-id="031c2-139">사용 하 여 `CanWriteResult` 다음 조건이 true 인 경우:</span><span class="sxs-lookup"><span data-stu-id="031c2-139">Use `CanWriteResult` if the following conditions are true:</span></span>

  * <span data-ttu-id="031c2-140">동작 메서드에서 모델 클래스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-140">Your action method returns a model class.</span></span>
  * <span data-ttu-id="031c2-141">런타임에 반환 될 수 있습니다는 파생된 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-141">There are derived classes which might be returned at runtime.</span></span>
  * <span data-ttu-id="031c2-142">알아야 파생 런타임 시 클래스 동작에 의해 반환 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-142">You need to know at runtime which derived class was returned by the action.</span></span>  

<span data-ttu-id="031c2-143">예를 들어, 작업 메서드 서명이 반환는 `Person` 종류와 반환할 수 있습니다는 `Student` 또는 `Instructor` 에서 파생 된 형식 `Person`합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-143">For example, suppose your action method signature returns a `Person` type, but it may return a `Student` or `Instructor` type that derives from `Person`.</span></span> <span data-ttu-id="031c2-144">포맷터만 처리 하기를 원하는 경우 `Student` 개체의 유형을 확인 [개체](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) 에 제공 된 컨텍스트 개체에는 `CanWriteResult` 메서드.</span><span class="sxs-lookup"><span data-stu-id="031c2-144">If you want your formatter to handle only `Student` objects, check the type of [Object](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) in the context object provided to the `CanWriteResult` method.</span></span> <span data-ttu-id="031c2-145">사용 하는 `CanWriteResult` 동작 메서드가 반환 될 때 `IActionResult`;이 경우는 `CanWriteType` 메서드 런타임 형식을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-145">Note that it's not necessary to use `CanWriteResult` when the action method returns `IActionResult`; in that case, the `CanWriteType` method receives the runtime type.</span></span>

<a id="read-write"></a>
### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a><span data-ttu-id="031c2-146">ReadRequestBodyAsync/WriteResponseBodyAsync 재정의</span><span class="sxs-lookup"><span data-stu-id="031c2-146">Override ReadRequestBodyAsync/WriteResponseBodyAsync</span></span> 

<span data-ttu-id="031c2-147">역직렬화 하는 동안 또는에 직렬화 하는 작업의 실제 작업을 수행 하면 `ReadRequestBodyAsync` 또는 `WriteResponseBodyAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-147">You do the actual work of deserializing or serializing in `ReadRequestBodyAsync` or `WriteResponseBodyAsync`.</span></span>  <span data-ttu-id="031c2-148">다음 예제에서 강조 표시 된 줄 종속성 주입 컨테이너 (가져올 수 없습니다을 생성자 매개 변수에서)에서 서비스를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-148">The highlighted lines in the following example show how to get services from the dependency injection container (you can't get them from constructor parameters).</span></span>

[!code-csharp[Main](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a><span data-ttu-id="031c2-149">사용자 지정 포맷터를 사용 하는 MVC 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="031c2-149">How to configure MVC to use a custom formatter</span></span>
 
<span data-ttu-id="031c2-150">사용자 지정 포맷터를 사용 하려면 추가를 포맷터 클래스의 인스턴스는 `InputFormatters` 또는 `OutputFormatters` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-150">To use a custom formatter, add an instance of the formatter class to the `InputFormatters` or `OutputFormatters` collection.</span></span>

[!code-csharp[Main](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

<span data-ttu-id="031c2-151">포맷터는 삽입 순서 대로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-151">Formatters are evaluated in the order you insert them.</span></span> <span data-ttu-id="031c2-152">첫 번째 우선 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-152">The first one takes precedence.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="031c2-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="031c2-153">Next steps</span></span>

<span data-ttu-id="031c2-154">참조는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample)를 구현 하는 간단한 vCard 입력 및 출력 포맷터입니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-154">See the [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-formatters/sample), which implements simple vCard input and output formatters.</span></span>  <span data-ttu-id="031c2-155">응용 프로그램을 읽고 다음 예제와 같이 vCards 씁니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-155">The application reads and writes vCards that look like the following example:</span></span>

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

<span data-ttu-id="031c2-156">VCard 출력 응용 프로그램을 실행 하 고 vcard "헤더" 텍스트와 Accept Get 요청을 보내고에 표시 하려면 `http://localhost:63313/api/contacts/` (Visual Studio에서 실행) 하는 경우 또는 `http://localhost:5000/api/contacts/` (명령줄에서 실행) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="031c2-156">To see vCard output, run the application and send a Get request with Accept header "text/vcard" to `http://localhost:63313/api/contacts/` (when running from Visual Studio) or `http://localhost:5000/api/contacts/` (when running from the command line).</span></span>

<span data-ttu-id="031c2-157">VCard 연락처의 메모리 내 컬렉션에 추가 하려면 위의 예제에서는 형식으로 지정 하는 본문에서 vCard 텍스트로 Content-type 헤더가 "텍스트/vcard"와 동일한 URL에 Post 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="031c2-157">To add a vCard to the in-memory collection of contacts, send a Post request to the same URL, with Content-Type header "text/vcard" and with vCard text in the body, formatted like the example above.</span></span>