---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: "SignalR 사용자 연결에 매핑하면 | Microsoft Docs"
author: tfitzmac
description: "이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다. Patrick Fletcher이 도움말이 항목을 작성 하는 데 도움이 되었습니다. 이 항목에서 사용 되는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/30/2014
ms.topic: article
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9b50d8805beabbc48467e20331c7593de9bc4254
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="0565e-105">SignalR 사용자 연결에 매핑</span><span class="sxs-lookup"><span data-stu-id="0565e-105">Mapping SignalR Users to Connections</span></span>
====================
<span data-ttu-id="0565e-106">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0565e-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0565e-107">이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-107">This topic shows how to retain information about users and their connections.</span></span>
> 
> <span data-ttu-id="0565e-108">Patrick Fletcher이 도움말이 항목을 작성 하는 데 도움이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-108">Patrick Fletcher helped write this topic.</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="0565e-109">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="0565e-109">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="0565e-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0565e-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="0565e-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="0565e-111">.NET 4.5</span></span>
> - <span data-ttu-id="0565e-112">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="0565e-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="0565e-113">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="0565e-113">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="0565e-114">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="0565e-115">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="0565e-115">Questions and comments</span></span>
> 
> <span data-ttu-id="0565e-116">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="0565e-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="0565e-117">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="introduction"></a><span data-ttu-id="0565e-118">소개</span><span class="sxs-lookup"><span data-stu-id="0565e-118">Introduction</span></span>

<span data-ttu-id="0565e-119">허브에 연결 되는 각 클라이언트 고유 연결 id를 전달 합니다. 이 값을 검색할 수 있습니다는 `Context.ConnectionId` 허브 컨텍스트 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="0565e-120">응용 프로그램을 사용자 연결 id에 매핑한 매핑이 유지 하는 경우에 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="0565e-121">사용자 ID 공급자 (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="0565e-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="0565e-122">[메모리 내 저장소](#inmemory), 사전 등</span><span class="sxs-lookup"><span data-stu-id="0565e-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="0565e-123">각 사용자에 대 한 SignalR 그룹</span><span class="sxs-lookup"><span data-stu-id="0565e-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="0565e-124">[세션에서 외부 저장소](#database)데이터베이스 테이블 또는 Azure 테이블 저장소와 같은</span><span class="sxs-lookup"><span data-stu-id="0565e-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="0565e-125">각각의이 구현은이 항목에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="0565e-126">사용 된 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 의 메서드는 `Hub` 사용자 연결 상태를 추적 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="0565e-127">가장 좋은 방법은 응용 프로그램에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="0565e-128">응용 프로그램을 호스팅하는 웹 서버의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="0565e-129">현재 연결 된 사용자 목록을 가져와서 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="0565e-130">응용 프로그램 또는 서버를 다시 시작 하는 경우에 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="0565e-131">외부 서버를 호출 하 여 대기 시간 문제 인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="0565e-132">다음 표에서 이러한 고려 사항에 대해 작동 하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="0565e-133">둘 이상의 서버</span><span class="sxs-lookup"><span data-stu-id="0565e-133">More than one server</span></span> | <span data-ttu-id="0565e-134">현재 연결 된 사용자 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-134">Get list of currently connected users</span></span> | <span data-ttu-id="0565e-135">다시 시작한 다음 정보를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-135">Persist information after restarts</span></span> | <span data-ttu-id="0565e-136">최적의 성능</span><span class="sxs-lookup"><span data-stu-id="0565e-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0565e-137">사용자 Id 공급자</span><span class="sxs-lookup"><span data-stu-id="0565e-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="0565e-138">메모리 내</span><span class="sxs-lookup"><span data-stu-id="0565e-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="0565e-139">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="0565e-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="0565e-140">영구 외부</span><span class="sxs-lookup"><span data-stu-id="0565e-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="0565e-141">IUserID 공급자</span><span class="sxs-lookup"><span data-stu-id="0565e-141">IUserID provider</span></span>

<span data-ttu-id="0565e-142">사용자 대상을 지정 하는 사용자 Id는이 기능을 통해 IUserIdProvider 새 인터페이스를 통해 IRequest에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="0565e-143">**IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="0565e-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="0565e-144">기본적으로 있을 것을 사용자의 사용 하는 구현 `IPrincipal.Identity.Name` 사용자 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="0565e-145">이 변경 하려면 등록의 구현 `IUserIdProvider` 전역 호스트 응용 프로그램 시작 시와:</span><span class="sxs-lookup"><span data-stu-id="0565e-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="0565e-146">허브에 내 수는 다음 API 통해 이러한 사용자에 메시지를 보낼:</span><span class="sxs-lookup"><span data-stu-id="0565e-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="0565e-147">**특정 사용자에 게 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="0565e-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="0565e-148">메모리 내 저장소</span><span class="sxs-lookup"><span data-stu-id="0565e-148">In-memory storage</span></span>

<span data-ttu-id="0565e-149">다음 예제는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="0565e-150">사전을 사용 하 여 한 `HashSet` 연결 id를 저장할 수 있습니다. 언제 든 지 사용자 SignalR 응용 프로그램에 둘 이상의 연결이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="0565e-151">예를 들어 사용자가 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 둘 이상의 연결 id는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="0565e-152">응용 프로그램이 종료 되 면 모든 정보가 손실 되 있지만 다시 채워집니다 사용자가 연결을 다시 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="0565e-153">환경의 각 서버 연결의 별도 컬렉션을 갖기 때문에 둘 이상의 웹 서버를 포함 하는 경우에 메모리 내 저장소 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="0565e-154">첫 번째 예에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="0565e-155">HashSet에 대 한 키를 사용자의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="0565e-156">다음 예에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="0565e-157">클래스의 인스턴스는 변수 이름에 저장 된 `_connections`합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="0565e-158">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="0565e-158">Single-user groups</span></span>

<span data-ttu-id="0565e-159">각 사용자에 대 한 그룹을 만들고에 해당 사용자만 액세스 하려는 경우 해당 그룹에는 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="0565e-160">각 그룹의 이름은 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="0565e-161">사용자에 게 둘 이상의 연결을 경우 각 연결 id는 사용자의 그룹에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="0565e-162">하지 수동으로 제거 해야 사용자 그룹에서 사용자 연결을 끊을 때.</span><span class="sxs-lookup"><span data-stu-id="0565e-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="0565e-163">이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="0565e-164">다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="0565e-165">세션에서 외부 저장소</span><span class="sxs-lookup"><span data-stu-id="0565e-165">Permanent, external storage</span></span>

<span data-ttu-id="0565e-166">이 항목에서는 연결 정보를 저장 하기 위한 데이터베이스 또는 Azure 테이블 저장소를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="0565e-167">이 방법은 각 웹 서버는 동일한 데이터 저장소와 상호 작용할 수 때문에 웹 서버가 여러 개 있는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="0565e-168">웹 서버 또는 응용 프로그램 다시 시작 하는 작업을 중지 하는 경우는 `OnDisconnected` 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="0565e-169">따라서 것이 데이터 저장소에 더 이상 사용할 수 있는 연결 id에 대 한 레코드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="0565e-170">이러한 분리 된 레코드를 정리 하려면 응용 프로그램에 관련 된 시간 범위 외부에서 생성 된 모든 연결을 무효화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="0565e-171">이 섹션의 예에서는 연결을 만들 때 추적에 대 한 값이 포함 되지만 백그라운드 작업으로 작업을 수행 하는 것이 좋습니다 때문에 오래 된 레코드를 정리 하는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="0565e-172">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="0565e-172">Database</span></span>

<span data-ttu-id="0565e-173">다음 예에서는 데이터베이스에 연결 및 사용자 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="0565e-174">모든 데이터 액세스 기술; 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="0565e-175">이러한 엔터티 모델 데이터베이스 테이블 및 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="0565e-176">데이터 구조에 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="0565e-177">첫 번째 예에는 많은 연결 엔터티와 연결할 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="0565e-178">그런 다음 허브에서 아래에 표시 된 코드와 함께 각 연결의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="0565e-179">Azure 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="0565e-179">Azure table storage</span></span>

<span data-ttu-id="0565e-180">다음 Azure 테이블 저장소 예제 데이터베이스 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="0565e-181">Azure 테이블 저장소 서비스를 시작 해야 하는 정보를 모두 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="0565e-182">자세한 내용은 참조 [.NET에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-how-to-use-tables/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="0565e-183">다음 예제에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="0565e-184">사용자 이름으로 데이터를 분할 하 고 사용자는 언제 든 지 여러 개의 연결이 있을 수 있으므로 각 엔터티에 연결 id로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="0565e-185">허브에서 각 사용자의 연결 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0565e-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]