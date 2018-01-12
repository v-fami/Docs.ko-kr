---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: "확장 및 축소 된 패널 JavaScript (VB)에서 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 및 확장 하는 기능과 제공는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 6adca6771042cad71139977496f985cb8dac63aa
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a><span data-ttu-id="c4e55-103">확장 및 JavaScript (VB)에서 패널 축소</span><span class="sxs-lookup"><span data-stu-id="c4e55-103">Collapsing and Expanding a Panel from JavaScript (VB)</span></span>
====================
<span data-ttu-id="c4e55-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c4e55-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c4e55-105">[코드를 다운로드](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c4e55-105">[Download Code](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)</span></span>

> <span data-ttu-id="c4e55-106">패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능과 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="c4e55-107">사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-107">These two actions can also be triggered from custom JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="c4e55-108">개요</span><span class="sxs-lookup"><span data-stu-id="c4e55-108">Overview</span></span>

<span data-ttu-id="c4e55-109">패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능과 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="c4e55-110">사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="c4e55-111">단계</span><span class="sxs-lookup"><span data-stu-id="c4e55-111">Steps</span></span>

<span data-ttu-id="c4e55-112">새 ASP.NET 페이지를 만들고 포함 우선,는 `ScriptManager` 한 내 `<form>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="c4e55-113">컨트롤 도구 키트에서 필요한 ASP.NET AJAX 라이브러리를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="c4e55-114">그런 다음 확장/축소 효과 볼 수 있도록 일부 텍스트와 패널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="c4e55-115">볼 수 있듯이 패널은 같습니다. (및 기본적으로 배경색 및 패널의 너비를 정의)는 CSS 클래스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

<span data-ttu-id="c4e55-116">`CollapsiblePanelExtender` 컨트롤을 사용 하려면는 `TargetControlID` 도구 키트 요청에 따라 확장 하거나 축소 패널을 알 수 있도록 특성:</span><span class="sxs-lookup"><span data-stu-id="c4e55-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

<span data-ttu-id="c4e55-117">그러나 현재 extender 축소 또는 패널을 확장에 대 한 특정 API를 노출 하지 않습니다 하지만 일부 문서화 되지 않은 메서드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="c4e55-118">우선, 패널의 콘텐츠를 확장 하거나 축소 클라이언트 쪽 JavaScript 트리거되고 다음 페이지에 세 개의 HTML 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="c4e55-119">클라이언트 쪽 JavaScript 코드에서 (시작 `<script type="text/javascript">`), `$find()` 메서드를 사용 해야 합니다. 액세스 하는 `CollapsiblePanelExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="c4e55-120">`$find("cpe")`에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="c4e55-121">이 위치에서 관련 메서드는 작업에 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="c4e55-122">메서드가 패널 (확장)을 열기 위해 호출 됩니다 `_doOpen()`; 다음 구현 코드는 `doOpen()` 함수는 첫 번째 단추를 클릭할 때 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

<span data-ttu-id="c4e55-123">패널을 축소 하거나 닫거나에 대 한는 `_doClose()` 메서드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="c4e55-124">따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

<span data-ttu-id="c4e55-125">세 번째 단추 패널의 상태를 전환:에서 축소 하 여 확장 하 고, 그 반대의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="c4e55-126">`CollapsiblePanelExtender` 노출 된 `toggle()` 정확히 일치 하는 메서드: 패널의 상태를 반대로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="c4e55-127">그러나 또한 다른 방법이 (내부적으로 사용 되는 `toggle()` 메서드):는 `get_Collapsed()` 의 메서드는 `CollapsiblePanelExtender()` 패널 축소 되는지 여부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4e55-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="c4e55-128">이 함수의 반환 값에 따라 패널은 하나 확장 한 다음 (`_doOpen()` 메서드) 또는 축소 된 (`_doClose()`) 방법:</span><span class="sxs-lookup"><span data-stu-id="c4e55-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]


<span data-ttu-id="c4e55-129">[![패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 코드 확장 되 고 뒤로](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c4e55-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="c4e55-130">패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 코드 확장 되어 백 ([전체 크기 이미지를 보려면 클릭](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c4e55-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="c4e55-131">이전</span><span class="sxs-lookup"><span data-stu-id="c4e55-131">Previous</span></span>](collapsing-and-expanding-a-panel-from-javascript-cs.md)